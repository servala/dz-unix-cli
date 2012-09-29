## Домашнее задание: [Unix Command Line](https://github.com/yandex-shri/lectures/blob/master/04-unix-cli.md)

Написать сценарий, который находит все файлы не входящие в SVN/Git и перемещает их в ~/.Trash/.

    git ls-files . --exclude-standard --others -z | xargs -0 -I {} mv {} ~/.Trash/

присылайте пулл реквесты с решением для SVN или с более элегантным подходом.

См. также: [пост про домашние задания](http://clubs.ya.ru/4611686018427468886/replies.xml?item_no=450).

Итак вот еще раз мое решение.

//делаем директории - выбираем файлы, вырезаем пути, по путям строим дирректории ( тестила в гит баш )
		<code>

	git status -s --untracked-files=all --porcelain | sed 's/?? //' | sed 's/\/[^/]*$/\//' | grep '/' | xargs -i mkdir ~/.Trash/{} 
	
	( для осьХ)
	git status -s --untracked-files=all --porcelain | sed 's/?? //' | sed 's/\/[^/]*$/\//' | grep '/' |xargs -I '{}' mkdir ~/.Trash/{}
		
		</code>

//перемещаем файлы (гит баш)
		<code>

	git status -s --untracked-files=all --porcelain | sed 's/?? //' | xargs -i mv {} ~/.Trash/{}
		
		</code>