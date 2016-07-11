#Linux
于2016/7/5开始自学《**Linux Shell Scripting Cookbook**》

Bash:	Bourne Again Shell

Shebang:	#!

###echo
	echo "Welcome to Bash"
	echo Welcomıe to Bash
	echo 'text in quotes'
	echo Hello World !
	echo "Hello World\!"
	printf "Hello\ World"
	
	printf "%-5s %-10s %-4s \n" No name Mark
	printf "%-5s %-10s %-4.2f \n" 1 Sarath 80.3456
	printf "%-5s %-10s %-4.2f \n" 2 James 90.9989
	printf "%-5s %-10s %-4.2f \n" 3 Jeff 77.564
	
	echo -e "1\t2\t3"
	
	颜色：重置=0，黑色=30,红色=31,绿色=32,黄色=33,蓝色=34,洋色=35,青色=36,白色=37
	echo -e "\e[1;31m This is red text \e[0m"
	彩色背景：重置=0，黑色=40,红色=41,绿色=42,黄色=43,蓝色=44,洋色=45,青色=46,白色=47
	echo -e "\e[1;42m Green Background \e[0m"
	
###赋值
	var=value(不包含空格)
	
	var="value"
	echo $var
	或者echo ${var}		曾经记得后者更佳！
	
	fruit=apple
	count=5
	echo "We have $count ${fruit}(s)"
	
	echo $PATH
	
	添加路径
	export PATH="$PATH:/home/user/bin"
	或者
	PATH="$PATH:/home/user/bin"
	export PATH
	
###获取长度
	length=${#var}
	
	e.g.
		var=123456
		echo ${#var}

###识别Shell
	echo $SHELL
	或者
	echo $0
	
###识别超级用户
	if [$UID -ne 0]; then
		echo Non root user.Please run as root.
	else
		echo Root user.
	fi
	测试上有问题

###数学运算 (let 、\$[ ]、\$(( ))、expr 、bc)
	
	n1=3;
	n2=5;
	let result=n1+n2
	echo $result
	let n1+=6
	let n1-=6
	result=$[n1+n2]
	result=$[$n1+5]
	result=$((n1+5))
	result=`expr 3 + 4` 注意空格
	result=$(expr $n1 + 5)
	echo "4 * 0.56" |bc
	result=`echo "$n1 * 1.5" |bc `
	小数精度:scale
	echo "scale=2;3/8" |bc
	进制转换
	echo "obase=2;100" |bc
	echo "obase=10;ibase=2;1100100" |bc
	echo "sqrt(100)" |bc
	echo "10^3" |bc
	
###文件描述符
- 0------stdin=-
- 1------stdout=/dev/stdout
- 2------stderr=/dev/stderr

###文件重定向（>、>>）
	写入
		echo "I go to Princeton" >a.txt
	追加
		echo "I go to Stanford" >>a.txt
	查看
		cat a.txt
	stderr重定向
		ls + 2>b.txt
	stderr、stdout单独重定向
		cmd 2>b.txt 1>a.txt
	stderr、stdout单独重定向
		cmd &> a.txt
	权限“读－写－执行”
		echo a1>a1
		cp a1 a2
		cp a2 a3
		chmod 000 a1
	tee重定向（-a 表示的是追加）
		cmd |tee file
		cat a.txt |tee b.txt |cat -n
		cat a.txt |tee -a b.txt |cat -n
		-表示stdin
			echo who is this | tee -|cat -n
	
	cat file|cmd
	cmd1 |cmd
	cmd < file
	
	文本块重定向
		cat<<EOF>a.txt
	另外，可以使用exec进行创建文件描述符

###数组
	array_var=(1 2 3 4 5 6)
	打印其中一个元素
		echo ${array_var[0]}
	打印所有元素
		echo ${array_var[*]}
		echo ${array_var[@]}
	个数
		echo ${#array_var[*]}
###关联数组
	declare -A ass_array
	ass_array=([index1]=val1 [index2]=val2)
	
	ass_array[index1]=val1
	ass_array[index2]=val2
	
	e.g.
		declare -A fruits_value
			//Mac 上不用声明！
		fruits_value=([apple]='100 dollars' [orange]='150 dollars')
		echo "Apple costs ${fruits_value[apple]}"
		
		echo ${!array_var[*]}
		echo ${!array_var[@]}
		e.g.
			echo ${!fruits_value[*]}
		
###别名alias
	alias new_cmd='cmd seq'
	
###文件改名（sed）
	for i in `cat ***.txt`
	do
		echo $i|sed "s/...$/***"
	done
	在文件的最后进行更改