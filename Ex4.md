* 变量（variable）

* -下划线（underscore），这个字符在变量里通常被用作假想的空格，用来隔开单词

` 
Traceback (most recent call last):
		File "ex4.py", line 8, in <module>
			average_passengers_per_car = car_pool_capacity / passenger
	NameError: name 'car_pool_capacity' is not defined
`

错误分析：变量名错误，在程序的第八行，变量'car_pool_capcity'没有找到，变量名书写错误，导致引用的变量无法识别

* 浮点数