//tv 볼륨이랑 채널, 꺼진지켜진지 등등 조절하는거(꺼지면 채널이랑 볼륨조절 불가능하게)

public class TestMyTV0 {
 	static void print_tv(MyTV0 t) {
 	if (t.isOn())
 		System.out.println("CH:"+t.getChannel()+" VOL:"+t.getVolume());
	else System.out.println("TV_OFF");
 	}
 	public static void main(String args[]) {
 		MyTV2 t = new MyTV2();
 		t.setChannel(100);
 		t.setVolume(0);
 		print_tv(t);
 		t.turnOnOff();
 		t.raiseChannel();
 		t.raiseVolume();
 		print_tv(t);
 		t.setChannel(10);
 		t.setVolume(100);
 		t.lowerChannel();
 		t.lowerVolume();
 		print_tv(t);
 		t.turnOnOff();
 		t.lowerChannel();
 		t.lowerVolume();
 		print_tv(t);
 		t.turnOnOff();
 		t.setChannel(50);
 		print_tv(t);
 		t.gotoPrevChannel();
 		print_tv(t);
 		t.gotoPrevChannel();
 		print_tv(t);
 		t.lowerChannel();
 		t.lowerChannel();
 		print_tv(t);
		t.gotoPrevChannel();
 		print_tv(t);
 		t.gotoPrevChannel();
 		print_tv(t);
 	}
}
class MyTV0 {
 	private boolean isPowerOn;
 	private int channel;
 	private int volume;
	public static final int MAX_CHANNEL = 100;
 	public static final int MIN_CHANNEL = 1;
 	public static final int MAX_VOLUME = 100;
	public static final int MIN_VOLUME = 1;
	
	protected MyTV0(){
		isPowerOn = false;
		channel=MIN_CHANNEL;
		volume=MIN_VOLUME;
	}
	public boolean isOn(){return isPowerOn;}
	public void turnOn(){isPowerOn=true;}
	public void turnOff(){isPowerOn=false;}
	public int getChannel(){return channel;}
	public boolean setChannel(int channel){
		if ((channel<=MAX_CHANNEL)&&(channel>=MIN_CHANNEL)&&isOn()){
			this.channel = channel;
			return true;
		}
		else return false;
	}
	public int getVolume(){return volume;}
	public boolean setVolume(int volume){
		if ((volume<=MAX_VOLUME)&&(volume>=MIN_CHANNEL)&&isOn()){
			this.volume = volume;
			return true;
		}
		else return false;
	}
}

class MyTV1 extends MyTV0 {
	public void turnOnOff() { if ( isOn() ) turnOff(); else turnOn(); }
 	public void lowerChannel() { setChannel(getChannel()-1); }
 	public void raiseChannel() { setChannel(getChannel()+1); }
 	public void lowerVolume() { setVolume(getVolume()-1); }
 	public void raiseVolume() { setVolume(getVolume()+1); }
}
class MyTV2 extends MyTV1 {
	protected int previousChannel;
	
	public boolean setChannel(int channel){
		if(isOn()&&(channel<=MAX_CHANNEL)&&(channel>=MIN_CHANNEL)){
			previousChannel = getChannel();
			super.setChannel(channel);
			return true;
		}
		else return false;
	}

	public boolean gotoPrevChannel(){
		setChannel(previousChannel);
		return true;
	}
}
