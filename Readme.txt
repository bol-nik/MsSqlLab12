Лабораторная работа №12
1.	Создать триггер, запрещающий обновление и удаление данных в таблице SALE в выходные и в праздничные дни.


Пример 1. Работа функции RAISERROR
a)	raiserror('This is message %s %d.', 
10,1, 'number', 5)
Result: This is message number 5.
b)	raiserror('<<%7.3s>>', 10,1, 'abcde')
Result: <<    abc>>
c)	raiserror('<<%*.*s>>', 10,1,7,3,'abcde')
Result: <<    abc>>


Пример 2. Запрет на ввод и изменение данных в таблице sale после 15 числа текущего месяца.
create trigger ins_sale on sale
for insert, update
as
declare @nDayOfMonth tinyint
select @nDayOfMonth=DatePart(dd,i.data)from sale s, Inserted i
where s.c_id=i.c_id and
s.p_id=i.p_id and
s.sp_id=i.sp_id and
s.qty=i.qty;
if @nDayOfMonth >15
Begin
ROLLBACK TRAN
RAISERROR('Day of Month >15', 12, 1)
end



