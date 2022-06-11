# dragon-book-front-python
重写龙书编译原理前端代码,python实现
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
        | 	do stmt while (bool);
        |	break;
        |	block
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