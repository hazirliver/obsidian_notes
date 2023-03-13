Для изучения возможностей создания воспроизводимых пайлпайнов с использованием dvc, воспользуемся примерами кода и данных из официальной документации
* Качаем данные
	`dvc get https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml`
* Качаем код из примера
	1. `wget https://code.dvc.org/get-started/code.zip`
	2. `unzip code.zip`
	3. `rm -rf code.zip`
	4. `pip install -r src/requirements.txt`
* Можем посмотреть, какие файлы у нас теперь есть:
	![[files_tree.png]]

0. Для начала начнем трекать наши файлы
	1. Отслеживание кода
		* `git add src/evaluate.py src/featurization.py src/prepare.py src/requirements.txt src/train.py`
		* `git commit -m "Start tracking pipeline's source code"`
	2. Отслеживание данных
		* `dvc add data/data.xml`
		* `git add data/data.xml.dvc`
		* `git commit -m "Start tracking src/data.xml via dvc"`
		  

1. Добавим первый этап нашего пайплайна -- препроцессинг данных
	* `dvc stage add -n prepare -p prepare.seed,prepare.split -d src/prepare.py -d data/data.xml -o data/prepared python src/prepare.py data/data.xml`
	* Должны получить что-то такое:
		![[dvc_stage_add_prepare.png]]
	* Давайте посмотрим на сформированный файл `dvc.yaml`
		![[dvc_yaml_at_first_stage.png]]
	* Теперь можем лучше понять смысл аргументов, которые задавали для добавления первого этапа пайплайна:
		* `-n prepare` -- имя этапа (stage)
		* `-p prepare.seed,prepare.split` -- можем отдельно фиксировать все гиперпараметры с помощью файла `params.yaml`. Обязательно писать их через запятую без пробела
			![[params_yaml_prepare_stage.png]]
		* `-d src/prepare.py -d data/data.xml` -- все зависимости, которые нужны данному этапу пайплайна. Тут нужно перечислить и данные и код, чтобы была возможность поймать любое изменение как в коде, так и в самих данных
		* `-o data/prepared` -- путь до аутпута данного этапа пайплайна
		* `pytohn src/prepare.py data/data.xml` -- комманда для запуска данного стейджа
	* Уже сейчас можем воспроизвести наш "пайплайн", пока состоящий из всего одного этапа:
		`dvc repro`
2. Добавим второй этап пайплайна
	1. `dvc run -n featurize -p featurize.max_features,featurize.ngrams -d src/featurization.py -d data/prepared -o data/features python src/featurization.py data/prepared data/features`
		![[dvc_yaml_at_second_stage.png]]
3. Добавлять этапы пайплайна не обязательно, используя команду `dvc run`. Мы можем сделать это вручную, редактируя `dvc.yaml`
	* Добавим этап обучения модели вручную в файл `dvc.yaml`
		![[dvc_yaml_at_third_stage.png]]
	
4. Теперь можем запустить `dvc repro`, чтобы воспроизвести весь пайплайн
	* В моем случае все этапы уже закэшированы и выглядит это вот так:
		![[dvc_repro_chached_case.png]]
		* Это позволяет сохранять вычислительные ресурсы, не пересчитывая этапы, которые не изменились
5. Посмотрим, как изменится поведение `dvc repro`, если мы, например, поменяем какой-то из параметров пайплайна, описанных в файле `params.yaml`
	* Выставим `n_est: 200` в этапе обучения модели
		![[params_yaml_changed.png]]
	* Еще раз запустим `dvc repro`
		![[dvc_repro_with_changed_param.png]]
		* Видим, что первые два этапа не запускались, так как никак не поменялись, однако этап с обучением модели был перезапущен, а также результаты были добавлены в кэш
		* Можем посмотреть `dvc.lock`, который содержит хэши инпутов и аутпутов этапов пайплайна
			![[dvc_lock.png]]
6. Наконец, можем посмотреть DAG нашего пайплайна с помощью команды `dvc dag`
	![[dvc_dag.png]]
	
	