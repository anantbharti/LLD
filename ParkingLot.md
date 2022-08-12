Design a parking lot using object-oriented principles.

Size.java
```java
public enum Size {
	SMALL,COMPACT,LARGE;
}
```
Slot.java
```java
public class Slot {
	
	private Size slotSize;
	private int level;
	private int position;
	private boolean isFree;
	private Vehicle parkedVehicle;
	
	public Slot(Size slotSize, int level, int position) {
		this.slotSize = slotSize;
		this.level = level;
		this.position = position;
		this.isFree = true;
		this.parkedVehicle = null;
	}

	public Size getSlotSize() {
		return slotSize;
	}

	public String getSlotDetail() {
		String ans = slotSize.name() + " slot at [ lev: "+ level + ", pos: "+position + "]";
		return ans;
	}
	
	public boolean isFree() {
		return isFree;
	}

	public void setFree(boolean isFree) {
		this.isFree = isFree;
	}

	public Vehicle getParkedVehicle() {
		return parkedVehicle;
	}

	public void setParkedVehicle(Vehicle parkedVehicle) {
		this.parkedVehicle = parkedVehicle;
	}
}
```
Vehicle.java
```java
public class Vehicle {
	private String number;
	private Size vehicleSize;
	private Slot parkingSlot;
	
	public Vehicle(String number,Size vehicleSize) {
		this.number = number;
		this.vehicleSize = vehicleSize;
		this.parkingSlot = null;
	}

	public String getNumber() {
		return number;
	}

	public Size getVehicleSize() {
		return vehicleSize;
	}

	public Slot getParkingSlot() {
		return parkingSlot;
	}

	public void setParkingSlot(Slot parkingSlot) {
		this.parkingSlot = parkingSlot;
	}
}
```
Bike.java
```java
public class Bike extends Vehicle{

	public Bike(String number) {
		super(number, Size.SMALL);
		
	}
}
```
Car.java
```java
public class Car extends Vehicle {

	public Car(String number) {
		super(number, Size.COMPACT);
	}
}
```
Bus.java
```java
public class Bus extends Vehicle{

	public Bus(String number) {
		super(number, Size.LARGE);
	}
}
```
Main.java
```java
import java.util.*;

public class Main {

	public static void main(String[] args) {
		
		ParkingLot parkingLot = ParkingLot.getInstance();
		
		for(int i=1;i<=5;i++)
		{
			parkingLot.addSlot(new Slot(Size.SMALL,i-1,i));
			parkingLot.addSlot(new Slot(Size.COMPACT,i-1,i));
			parkingLot.addSlot(new Slot(Size.LARGE,i-1,i));
		}
		
		parkingLot.showAvailableSlots();
		
		List<Vehicle> vehicles =  new ArrayList<Vehicle>();
		for(int i=1;i<=8;i++)
		{
			vehicles.add(new Bike("JH01-"+i*2001));
			vehicles.add(new Car("JH02-"+i*2002));
			vehicles.add(new Bus("JH05-"+i*2005));
		}
		
		int i=0,j=0;
		
		while(i<vehicles.size()) {
			
			try {
				parkingLot.parkVehicle(vehicles.get(i));
				i++;
			}
			catch(Exception e1) {
				
				System.out.println(e1.getMessage());
				
				try {
					parkingLot.unparkVehicle(vehicles.get(j));
					j++;
				}
				catch(Exception e2) {
					System.out.println(e2.getMessage());
					break;
				}
			}
		}
		
		while(j<vehicles.size()) {
			
			try {
				parkingLot.unparkVehicle(vehicles.get(j));
			}
			catch(Exception e2) {
				System.out.println(e2.getMessage());
			}
			j++;
		}
		
		parkingLot.showAvailableSlots();
	}
}
```

Output
```
Available slots: 
SMALL:   5
COMPACT: 5
LARGE:   5
SMALL slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH01-2001
COMPACT slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH02-2002
LARGE slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH05-2005
SMALL slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH01-4002
COMPACT slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH02-4004
LARGE slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH05-4010
SMALL slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH01-6003
COMPACT slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH02-6006
LARGE slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH05-6015
SMALL slot at [ lev: 3, pos: 4] is alotted to vehicle no: JH01-8004
COMPACT slot at [ lev: 3, pos: 4] is alotted to vehicle no: JH02-8008
LARGE slot at [ lev: 3, pos: 4] is alotted to vehicle no: JH05-8020
SMALL slot at [ lev: 4, pos: 5] is alotted to vehicle no: JH01-10005
COMPACT slot at [ lev: 4, pos: 5] is alotted to vehicle no: JH02-10010
LARGE slot at [ lev: 4, pos: 5] is alotted to vehicle no: JH05-10025
No SMALL slot is available for vehicle JH01-12006
Vehicle JH01-2001 is unparked. SMALL slot at [ lev: 0, pos: 1] is available.
SMALL slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH01-12006
No COMPACT slot is available for vehicle JH02-12012
Vehicle JH02-2002 is unparked. COMPACT slot at [ lev: 0, pos: 1] is available.
COMPACT slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH02-12012
No LARGE slot is available for vehicle JH05-12030
Vehicle JH05-2005 is unparked. LARGE slot at [ lev: 0, pos: 1] is available.
LARGE slot at [ lev: 0, pos: 1] is alotted to vehicle no: JH05-12030
No SMALL slot is available for vehicle JH01-14007
Vehicle JH01-4002 is unparked. SMALL slot at [ lev: 1, pos: 2] is available.
SMALL slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH01-14007
No COMPACT slot is available for vehicle JH02-14014
Vehicle JH02-4004 is unparked. COMPACT slot at [ lev: 1, pos: 2] is available.
COMPACT slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH02-14014
No LARGE slot is available for vehicle JH05-14035
Vehicle JH05-4010 is unparked. LARGE slot at [ lev: 1, pos: 2] is available.
LARGE slot at [ lev: 1, pos: 2] is alotted to vehicle no: JH05-14035
No SMALL slot is available for vehicle JH01-16008
Vehicle JH01-6003 is unparked. SMALL slot at [ lev: 2, pos: 3] is available.
SMALL slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH01-16008
No COMPACT slot is available for vehicle JH02-16016
Vehicle JH02-6006 is unparked. COMPACT slot at [ lev: 2, pos: 3] is available.
COMPACT slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH02-16016
No LARGE slot is available for vehicle JH05-16040
Vehicle JH05-6015 is unparked. LARGE slot at [ lev: 2, pos: 3] is available.
LARGE slot at [ lev: 2, pos: 3] is alotted to vehicle no: JH05-16040
Vehicle JH01-8004 is unparked. SMALL slot at [ lev: 3, pos: 4] is available.
Vehicle JH02-8008 is unparked. COMPACT slot at [ lev: 3, pos: 4] is available.
Vehicle JH05-8020 is unparked. LARGE slot at [ lev: 3, pos: 4] is available.
Vehicle JH01-10005 is unparked. SMALL slot at [ lev: 4, pos: 5] is available.
Vehicle JH02-10010 is unparked. COMPACT slot at [ lev: 4, pos: 5] is available.
Vehicle JH05-10025 is unparked. LARGE slot at [ lev: 4, pos: 5] is available.
Vehicle JH01-12006 is unparked. SMALL slot at [ lev: 0, pos: 1] is available.
Vehicle JH02-12012 is unparked. COMPACT slot at [ lev: 0, pos: 1] is available.
Vehicle JH05-12030 is unparked. LARGE slot at [ lev: 0, pos: 1] is available.
Vehicle JH01-14007 is unparked. SMALL slot at [ lev: 1, pos: 2] is available.
Vehicle JH02-14014 is unparked. COMPACT slot at [ lev: 1, pos: 2] is available.
Vehicle JH05-14035 is unparked. LARGE slot at [ lev: 1, pos: 2] is available.
Vehicle JH01-16008 is unparked. SMALL slot at [ lev: 2, pos: 3] is available.
Vehicle JH02-16016 is unparked. COMPACT slot at [ lev: 2, pos: 3] is available.
Vehicle JH05-16040 is unparked. LARGE slot at [ lev: 2, pos: 3] is available.
Available slots: 
SMALL:   5
COMPACT: 5
LARGE:   5
```
