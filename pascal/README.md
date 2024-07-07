#### Free Pascal


```bash
# компиляция
$ fpc hello.pas
```
Пример программы
```pascal
program hello;  {комментарий}

const
	hello = 'Hello';
 	count = 20;
  	count2: integer = 20;
  
var
	x: integer = 500;
 	y: integer;
  	z: longint;
  	flag: boolean;
   
begin
	writln('Hello world!');
 	write('hello');
  	writeln('173 * 81 =', 173 * 81);	{ div, mod }
   	read(x);

   	x := 79;		{ оператор присваивания }

      	{ ветвление }
       if x > 0 then	{ (x > 0) and (y > 0) or (z > 0)	(bool = true) or (bool = false) }
		begin
		writeln('x > 0');
  		end
       else
       		begin
		writeln('x <= 0');
       		end;

  	{ цикл с предусловием }
   	while x < 20 do
    		begin
      		writeln(x);
    		x := x + 1;
      		end;

 	{ цикл с постусловием }
 	 x := 0;
  	repeat
		writeln(x);
    		x := x + 1;
   	until x < 20 ;

    	{ цикл for }
	for x := 0 to 20 do
		writeln(x);

  	{ побитовые операции }
   	x := not y;	{ shr, shl, and, or, not }
 
end.
```
