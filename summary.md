# 学习小结

## 问题汇总

- 遇到的一些问题记在本子上，也没有整理，一段时间过后再翻到某个问题，一时半会儿连自己都看不明白，没有养成一个好的学习习惯，很多时候都图省事

- 第一遍是跟着书上走的，代码写完对照着检查一遍，基本上运行结果都没有太大问题。

- 前25个练习很好理解，各代码意思都很明确；在练习25到练习41，代码中不断出现一些新的函数，书中也没有详细的解释，刚开始一头雾水，虽然输出的结果是正确的，但没有真正理解其中的意思。随着习题的不断深入，新的函数越来越多，最后才发现这些所谓的新函数都是python内置的

- 在习题40开始，代码的抽象程度越来越高，像面向对象编程这种概念很是不理解，看的很晕，短短的几行代码就给绕晕了

- 不少错误发生在符号错误或缺失，或是单词拼写错误
  不少练习中出现的函数都是书上没有解说的，要自己在网上去查，网上的坑不少，要么说的很简单要么就是整得很复杂，结果是问题解决了，时间花了不少；能阅读官方文档是最好的，无奈英语能力有限，也就简单的文档还能看懂一点

- 很多函数写完代码回头就忘了，我的解决办法是多次写代码实践，多看看别人写的代码，积累下来还是能记住不少常用的代码，下次看到至少知道       代码的意思，比如`pop()`删除列表元素，`append()`增加列表元素

- 仔细阅读常见问题答案往往能发现很多有趣的东西，会就练习中出现的一些问题进行解说

- 翻墙看了一下维基百科关于python的条目，其中很详细的解释了python的起源以及软件特性，有趣的是在python交互环境里输入 `>>>import this`,会弹出被叫做Python准则的‘Python格言’

- 在wiki中知道了有全局变量这个概念，书中对这个词只是一笔带过并没有详细解释（习题38：列表的操作）

## 解题过程（习题25）

ex25.py

	def break_words(stuff):
		"""This function will break up words for us."""
		words = stuff.split(' ')
		return words
	
	def sort_words(words):
		"""Sorts the words."""
		return sorted(words)
	
	def print_first_word(words):
		"""Prines the first word after popping it off."""
		word = words.pop(0)
		print word
	
	def print_last_word(words):
		"""Prints the last word after popping it off."""
		word = words.pop(-1)
		print word
	
	def sort_sentence(sentence):
		"""Takes in a full sentence and returns the sorted words."""
		words = break_words(sentence)
		return sort_words(words)
	
	def print_first_and_last(sentence):
		"""Prints the first and last words of the sentence."""
		words = break_words(sentence)
		print_first_word(words)
		print_last_word(words)
	
	def print_first_and_last_sorted(sentence):
		"""Sorts the words then prints the first and last one."""
		words = sort_sentence(sentence)
		print_first_word(words)
		print_last_word(words)

运行结果:

	Python 2.7.13 (v2.7.13:a06454b1afa1, Dec 17 2016, 20:42:59) [MSC v.1500 32 bit (Intel)] on win32
	Type "help", "copyright", "credits" or "license" for more information.
	>>> import ex25
	>>> sentence = "All good things come to those who wait."
	>>> words = ex25.break_words(sentence)
	>>> words
	['All', 'good', 'things', 'come', 'to', 'those', 'who', 'wait.']
	>>> sorted_words = ex25.sort_words(words)
	>>> sorted_words
	['All', 'come', 'good', 'things', 'those', 'to', 'wait.', 'who']
	>>> ex25.print_first_word(words)
	All
	>>> ex25.print_last_word(words)
	wait.
	>>> words
	['good', 'things', 'come', 'to', 'those', 'who']
	>>> ex25.print_first_word(sorted_words)
	All
	>>> ex25.print_last_word(sorted_words)
	who
	>>> sorted_words
	['come', 'good', 'things', 'those', 'to', 'wait.']
	>>> sorted_words = ex25.sort_sentence(sentence)
	>>> sorted_words
	['All', 'come', 'good', 'things', 'those', 'to', 'wait.', 'who']
	>>> ex25.print_first_and_last(sentence)
	All
	wait.
	>>> ex25.print_first_and_last_sorted(sentence)
	All
	who

- 遇到的问题

	1. 变量名的赋值
	2. 定义的函数及其作用
	3. 各函数之间的调用
	4. python交互环境的使用

- 解题思路

	- [研究答案中没有分析过的行，找出它们的来龙去脉](https://github.com/tickhcj/studydrills/blob/master/Ex25.md)

	- 在mystuff目录下进入python交互模式，这样才能读取ex25.py(如果要同时调取不同路径下的文件该如何呢）

	- 找出代码中python内置的函数 `split()` `sorted()` `pop()`,开始时一直没弄明白，为何没有定义过的函数在调用时却不报警呢，通过在网上搜索才明白这是python内置的函数

	- 定义函数的参数名称是可变的，在调用函数可以使用新的变量名 `sort_words(words)` 在使用时 `words = ex25.break_words(sentence)` ,返回得到的结果又可以赋值给新的变量
