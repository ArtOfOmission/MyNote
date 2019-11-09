```sql

begin try

	declare @i int=0;
	select 3/@i;

end try
begin catch
    select '错误消息：' ;
	select ERROR_LINE() as errorLine;   --返回错误行数
	select ERROR_MESSAGE() as errorMsg; --返回错误消息
	select ERROR_NUMBER() as errorNum;  --返回错误号
	select ERROR_SEVERITY() as errorSeverIty; --返回严重性
	select ERROR_PROCEDURE() errorProcedure;  --返回错误出现的存储过程或触发器
	select ERROR_STATE() errorState;--返回错误状态号
	
end catch

```