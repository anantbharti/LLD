Imagine you have a call center with three levels of employees: respondent, 
manager and director. An incoming telephone call must be first allocated to a 
respondent who is free. If the respondent can't handle the call, he or she must 
escalate the call to a manager. If the manager is not free or not able to handle it, 
then the call should be escalated to a director. Design the classes and data 
structures for this problem. Implement a method handleCaLL() which assigns a 
call to the first available employee.

Call.java
```java
public class Call {
	
	private String callId;
	private Employee callHandler;
	
	public Call(String callId) {
		this.callId = callId;
		this.callHandler = null;
	}
	
	public String getCallId() {
		return callId;
	}
	
	public void setCallHandler(Employee callHandler) {
		this.callHandler = callHandler;
	}
	
	public Employee getCallHandler() {
		return callHandler;
	}

}
```
Employee.java
```java
public class Employee {
	String name;
	int level;
	
	public Employee(String name,int level) {
		this.name = name;
		this.level = level;
	}

	public int getLevel() {
		return level;
	}

	public void setLevel(int level) {
		this.level = level;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}
	
}
```
Director.java
```java
public class Director extends Employee{

	public Director(String name) {
		super(name, 2);
	}
}
```

Manager.java
```java
public class Manager extends Employee {

	public Manager(String name) {
		super(name, 1);
	}
}
```

Respondent.java
```java
public class Respondent extends Employee{

	public Respondent(String name) {
		super(name, 0);
	}
}
```
CallHandler.java
```java
public class CallHandler {
	private List<List<Employee>> handlers;
	private static CallHandler instance;
	
	private CallHandler() {
		handlers = new ArrayList<List<Employee>>();
		
		for(int i=0;i<3;i++)
		{
			List<Employee> q = new ArrayList<Employee>();
			handlers.add(q);
		}
	}
	
	public static CallHandler getInstance() {
		if(instance != null)
			return instance;
		
		instance = new CallHandler();
		return instance;
	}
	
	public void addHandler(Employee handler) {
		int level = handler.getLevel();
		List<Employee> q = handlers.get(level);
		q.add(handler);
		handlers.set(level, q);
	}
	
	public void handleCall(Call call)throws Exception {
		for(int i=0;i<3;i++)
		{
			if(handlers.get(i).isEmpty())
				continue;
			List<Employee> q = handlers.get(i);
			Employee handler = q.remove(0);
			handlers.set(i, q);
			call.setCallHandler(handler);
			
			System.out.println(handler.getName()+" is handling call "+call.getCallId());
			
			break;
		}
		if(call.getCallHandler() == null)
			throw new Exception("Unable to handle call " + call.getCallId());
	}
	
	public void endCall(Call call)throws Exception {
		Employee handler = call.getCallHandler();
		
		if(handler == null)
			throw new Exception("Unhandled call "+call.getCallId());
		
		int level = handler.getLevel();
		List<Employee> q = handlers.get(level);
		q.add(handler);
		
		handlers.set(level, q);
		
		System.out.println("Call "+call.getCallId() + " ended. "+handler.getName()+" is available.");
	}
	
	public void showAvailableHandlers() {
		for(int i=0;i<3;i++)
		{
			if(handlers.get(i).isEmpty())
			{
				System.out.println("Level "+i+" is empty!");
				continue;
			}
			
			System.out.println("Level "+i);
			List<Employee> q = handlers.get(i);
			
			for(int j=0;j<q.size();j++)
				System.out.println(q.get(j).getName());
		}
	}
}
```

Main.java
```java
public class Main {

	public static void main(String[] args) {
		
		CallHandler callHandler = CallHandler.getInstance();
		
		callHandler.addHandler(new Respondent("Banty"));
		callHandler.addHandler(new Manager("Solty"));
		callHandler.addHandler(new Director("Monty"));
		
		
		List<Call> calls = new ArrayList<Call>();
		
		for(int i=0;i<10;i++)
		{
			Call c = new Call(i+"");
			calls.add(c);
		}
		
		int i = 0,j = 0;
		
		while(i<10)
		{
			try {
				callHandler.handleCall(calls.get(i));
				i++;
			}catch(Exception e1) {
				System.out.println(e1.getMessage());
				try {
					callHandler.endCall(calls.get(j));
					j++;
				}catch(Exception e2) {
					System.out.println(e2.getMessage());
				}
			}
		}
		
		while(j<10)
		{
			try {
				callHandler.endCall(calls.get(j));
				j++;
			}catch(Exception e2) {
				System.out.println(e2.getMessage());
			}
		}
		
	}

}
```
Output
```
Banty is handling call 0
Solty is handling call 1
Monty is handling call 2
Unable to handle call 3
Call 0 ended. Banty is available.
Banty is handling call 3
Unable to handle call 4
Call 1 ended. Solty is available.
Solty is handling call 4
Unable to handle call 5
Call 2 ended. Monty is available.
Monty is handling call 5
Unable to handle call 6
Call 3 ended. Banty is available.
Banty is handling call 6
Unable to handle call 7
Call 4 ended. Solty is available.
Solty is handling call 7
Unable to handle call 8
Call 5 ended. Monty is available.
Monty is handling call 8
Unable to handle call 9
Call 6 ended. Banty is available.
Banty is handling call 9
Call 7 ended. Solty is available.
Call 8 ended. Monty is available.
Call 9 ended. Banty is available.
```






