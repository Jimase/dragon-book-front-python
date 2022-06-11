# dragon-book-front-python
重写龙书编译原理前端代码,python实现 for hzf 编译实验
龙书的前端源码是java实现的，基于ll(1)递归下降分析法生成三地址码作为中间代码，本项目为其python实现
## 文法
```
program	->	block
block 	->	{ decls stmts }
decls 	->	decls decl | ε
decl 	->	type id;
type 	->	type [ num ] | basic
stmts 	->  stmts stmt | ε
stmt 	-> 	loc = bool;
        |	if (bool) stmt
        | 	if (bool) stmt else stmt
        | 	while (bool) stmt
        |   forstmt
        | 	do stmt while (bool);
        |	break;
        |	block
forstmt -> for ( forassign ; bool ; forassign ) stmts
loc 	->	loc [ bool ] | id
bool	-> 	bool || join | join
join 	-> 	join && equality | equality
equality->	equality == rel | equality != rel | rel
rel		-> 	expr < expr | expr <= expr | expr > expr | expr >= expr | expr
expr 	-> 	expr + term | expr - term | term
term 	-> 	term * unary | term / unary | unary
unary	-> 	!unary	| -unary | factory
factory ->	(bool) | loc | num | real | true | false
```

## USGE
``` python parser```
### input and uotput example
```C
    {
    int[10][20] a; int i;int j;int k;
    float b;float c;
    
    if( k<=1 && k<=2 || k <=3 && k<=4 || k<=5 && k<=6 || k<=7 && k<=8 || k<=9 && k<=10 ){
        b=19.19;
    }else{
        b = 10.11;
        for( i = 0; i<= 100 ; i=i+1){
            a[3][i-1] = 10;
            for(j = 0; j<=100; j=j+1){
                a[i][j] = a[i][j] + 1;
            }
            
        }
    }
}
```


```
L1:
	iffalse k <= 1 goto L7
	if k <= 2 goto L6
L7:
	iffalse k <= 3 goto L8
	if k <= 4 goto L6
L8:
	iffalse k <= 5 goto L9
	if k <= 6 goto L6
L9:
	iffalse k <= 7 goto L10
	if k <= 8 goto L6
L10:
	iffalse k <= 9 goto L5
	iffalse k <= 10 goto L5
L6:
L4:
	b = 19.19
L11:
	goto L3
L5:
	b = 10.11
L12:
	i = 0
L14:
	iffalse i <= 100 goto L13
	i = i + 1
	t1 = 3 * 80
	t2 = i - 1
	t3 = t2 * 4
	t4 = t1 + t3
	a [ t4 ] = 10
L15:
	j = 0
L17:
	iffalse j <= 100 goto L16
	j = j + 1
	t5 = i * 80
	t6 = j * 4
	t7 = t5 + t6
	t8 = i * 80
	t9 = j * 4
	t10 = t8 + t9
	t11 = a[t10]
	t12 = t11 + 1
	a [ t7 ] = t12
L18:
	goto L15
L16:
	goto L12
L13:
L3:
L2:
```
## todo-list
- [ ] 基本的类型检查(ll1递归已经是减分的作业做法了，还没全做。。)