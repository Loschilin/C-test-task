### С# test task

Есть интерфейс отчета
```
public interface IReport 
{
...
}
```

Есть несколько типов договоров
```
public abstract class Contract 
{
...
}
```
``` public abstract class LaborContract : Contract { ... } ```
``` public class MainContract : LaborContract { ... } ```
``` public class AdditionalContract : LaborContract { ... } ```
``` public class CivilContract : Contract { ... } ```

Каждый для каждого типа договора, создается определенный набор отчетов
**MainContract**
``` public class ReportMain1: IReport  { ... } ```
``` public class ReportMain2: IReport  { ... } ```

**AdditionalContract**
``` public class ReportAdditional1: IReport  { ... } ```
``` public class ReportAdditional2: IReport  { ... } ```

**CivilContract**
``` public class ReportAdditional1: IReport  { ... } ```
``` public class ReportAdditional2: IReport  { ... } ```

Есть интерфейс фабрики для создания отчетов в зависимости от типа договора
```
public interface IReportFactory
{
	IEnumerable<IReport> GetReport(Contract contract);
}
```

***Сделать реализацию фабрики IReportFactory***

Есть репозиторий 
```
public interface IEmployeeRepository
{
	void Save(Employee employee);
	void Delete(Employee employee);
	Employee Get(Guid companyId, Guid id);
	IEnumerable<Employee> GetList(Guid companyId);
}
```

есть реализаця 
```
public class SqlEmployeeRepository : IEmployeeRepository
{
	public void Save(Employee employee)
	{ ... } 
	
	public void Delete(Employee employee)
	{ ... } 
	
	Employee Get(Guid companyId, Guid id)
	{ ... }
	
	IEnumerable<Employee> GetList(Guid companyId)
	{ ... } 
}
```

В какой-то момент, понимаем, что получение сотрудников из хранилища начинает тормозить и решаем закешировать наших сотрудников.

Есть клиетн кэша с интерфейсом
```
public interface ICacheClient 
{
	void Add<T>(string key, T value);
	void Delete(string key);
	T Get<T>(string key);
	void HashAdd<T>(string key, string hashkey, T value);
	void HashDelete(string key, string hashkey);
	T HashGet<T>(string key, string hashkey);
	IEnumerable<T> HashGet(string key);
}
```
и его реализация
``` public class CacheRedisClient: ICacheClient {...} ```

Первые три метода работают как ключ значение. Метод исполюзующие Hash работают с данными типа ключ, ключ, значение.
Необходимо реализовать кеширование сущности Employee.

**Все реализации представить в виде PullRequest на GitHub.
Регистрацию зависимостей выполнить любым IoC.**
