## Facade ( 外观模式 ) ##

提供了一个统一的接口，用来访问子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。

设计原则：
“最少知识”原则（Least Knowledge）——就任何对象而言，在该对象的方法内，我们只应该调用属于以下范围的方法：

1. 该对象本身；
2. 被当做方法的参数而传递进来的对象；
3. 此方法所创建或实例化的任何对象；
4. 对象的任何组件。

### 示例代码 ###
    
    package com.designpattern.facade;
    public class HomeThreaterFacade {
    	Amplifier amp;		
    	Tuner tuner;
    	DvdPlayer dvd;		
    	CdPlayer cd;
    	Projector projector;	
    	ThreaterLights lights;
    	Screen screen;		
    	PopcornPopper popper;	
    
    	public HomeThreaterFacade(Amplifier amp,   Tuner tuner,	DvdPlayer dvd, CdPlayer cd, Projector projector, Screen screen, ThreaterLights lights, PopcornPopper popper)
    	{
    		this.amp = amp; 		
    		this.tuner = tuner;		
    		this.dvd = dvd; 		
    		this.cd = cd;
    		this.projector = projector;	
    		this.lights = lights;
    		this.screen = screen;	
    		this.popper = popper;	
    	}	
    	
    	
    	public void watchMovie(String movie){
    		System.out.println("Get ready to watch a movie...");
    		popper.on();	
    		popper.pop();
    		lights.dim(10);
    		screen.down();
    		projector.on();
    		projector.wideScreenMode();	
    		amp.on();
    		amp.setDvd();
    		amp.setSurroundSound();
    		amp.setVolume(5);
    		dvd.on();
    		dvd.play(movie);	}
    
    		public void endMovie(){	……}
    }
    
    
    