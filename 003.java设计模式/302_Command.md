## Command ( 命令模式 ) ##

将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。
我们知道一个命令各对象通过在特定接收者上绑定一组动作来封装一个请求。要达到这一点，命令对象将动作和接收者包进对象中。这个对象只暴露出一个execute()方法，当此方法被调用时，接收者就会进行这些动作。从外面来看，其他对象不知道究竟哪个接收者进行了哪些动作，只知道如果调用execute()方法，请求的目的就能达到。


    
    package com.designpattern.command;
    public interface Command {	
    	public void execute();	
    	public void undo();	
    }
    
    package com.designpattern.command;
    public class Light {	
    	private boolean on = false;	
    	public void on() {		
    		this.on = true;	
    	}	
    	public void off() {		
    		this.on = false;	
    	}	
    	public String getStatus() {		
    		if (on) {return "ON";} else {return "OFF";}	
    	}
    }

package com.designpattern.command;
public class OnCommand implements Command {
	private Light light;	
	public OnCommand(Light l) {
		this.light = l;	
	}	
	@Override	
	public void execute() {
		light.on();	
	}
	@Override	
	public void undo() {
		light.off();
		System.out.println("The light is off!");	
	}


    
    package com.designpattern.command;
    public class OffCommand implements Command {
    	private Light light;		
    	public OffCommand(Light l)
    	{
    		this.light = l;	
    	}
    	@Override
    	public void execute() 
    	{
    		light.off();	
    	}
    	@Override	
    	public void undo() 
    	{
    		light.on();
    		System.out.println("The light is on!");	
    	}
    }
    

    package com.designpattern.command;
    public class NoCommand implements Command {
    	@Override	
    	public void execute() {
    		// TODO Auto-generated method stub	
    	}
    	@Override	public void undo() {
    		// TODO Auto-generated method stub	
    	}
    }
    		
		
    package com.designpattern.command;
    public class Invoker {
    	private Command command;	
    	private Command undoCommand;
    	public Invoker() {
    		command = new NoCommand();
    		undoCommand = new NoCommand();	
    	}	
    	public void setCommand(Command c) {
    		this.command = c;	
    	}
    	public void pressButton() {
    		this.command.execute();
    		undoCommand = command;	
    	}
    	public void undoPress() {
    		undoCommand.undo();	
    	}
    }
    
    
    
    
    
	    
	
	package com.designpattern.command;
	public class Test {	
	/**	 * @param args	 */	
	public static void main(String[] args) {				
		Light light = new Light();				
		Command on = new OnCommand(light);
		Command off = new OffCommand(light);
		
		Invoker invoker = new Invoker();		
		invoker.setCommand(on);		
		invoker.pressButton();		
		invoker.undoPress();				
		System.out.println("Light  "+light.getStatus());
		}
	}
	
	
	
