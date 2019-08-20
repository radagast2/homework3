
import java.awt.EventQueue;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.time.LocalDate;
import java.util.Calendar;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextField;

/**
 * description：实现查询出生天数，下次生日，查询星座功能
 * @author 王昊
 *Create Date:2019-8-9

 */



@SuppressWarnings("serial")
public class thisTest extends JFrame{
	static int DEFAULT_HEIGHT=800;
	static int DEFAULT_WIDTH=600;
	//top组件
	private JLabel toplab=new JLabel("请输入你的出生日期",JLabel.CENTER);
	
	//mid组件
	private JPanel midpal=new JPanel();
	
	private JLabel midyear=new JLabel("年");
	private JLabel midmonth=new JLabel("月");
	private JLabel midday=new JLabel("日");
	
	private JTextField biryear= new JTextField(4);
	private JTextField birmonth= new JTextField(4);
	private JTextField birday= new JTextField(4);
	
	//bottom 组件
	private JPanel botpal=new JPanel();
	
	private JButton button1=new JButton("下个生日");
	private JButton button2=new JButton("出生天数");
	private JButton button3=new JButton("查询星座");
	
	
	//监视器
	private nextBirthday nextbirthday=new nextBirthday ();
	private dayOfBirth dayofBirth=new dayOfBirth();
	private serXz serxz=new serXz();
	
	//结果显示
	private JTextField result =new JTextField(12);
	private JPanel outpal=new JPanel();
	private JLabel resultlab=new JLabel("结果");
	
	
	
	//构造器
	public thisTest() {
		setLayout(new GridLayout(4,1));  //frame分为四行一列
		setSize(DEFAULT_HEIGHT,DEFAULT_WIDTH);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setVisible(true);
		setLocation(300,300);
		botpal.setLayout(new FlowLayout());
		midpal.setLayout(new FlowLayout());
		outpal.setLayout(new FlowLayout());
		
		//设置字体
		Font font=new Font("宋体",Font.BOLD,20);
		Font font1=new Font("宋体",Font.BOLD,30);
		toplab.setFont(font1);
		midyear.setFont(font);
		midmonth.setFont(font);
		midday.setFont(font);
		
		//添加
		this.add(toplab);
		
		midpal.add(biryear);
		midpal.add(midyear);
		midpal.add(birmonth);
		midpal.add(midmonth);
		midpal.add(birday);
		midpal.add(midday);
		
		addButton(button1,nextbirthday);
		addButton(button2,dayofBirth);
		addButton(button3,serxz);
		
		//结果显示
		outpal.add(resultlab);
		outpal.add(result);
		resultlab.setFont(font);//设置标签字体
		
		this.add(midpal);
		this.add(botpal);
		this.add(outpal);
		
		
	}
	
	//main方法
	public static void main(String[] args) {
		EventQueue.invokeLater(()->{
			@SuppressWarnings("unused")
			thisTest a=new thisTest();
		});

	}
	
	//确定输入正确格式
	
	public Boolean currectin(String year,String month,String day) {
		
		int thisyear=Integer.valueOf(year);
		int thismonth=Integer.valueOf(month);
		int thisday=Integer.valueOf(day);
		Calendar c = Calendar.getInstance();
		if((year.equals(""))||(month.equals(""))||(day.equals("")))//确定年月日都输入，运行结果错误
			return true;
		else if((thisyear<=0||thisyear>c.get(Calendar.YEAR))||(thismonth<=0||thismonth>12)||(thisday<=0||thisday>=32))//年月日规范
			return true;
		else 
			return false;
	}
	
	
	//出生天数
	public static String calculateTimeDifferenceByPeriod(int year, int month, int dayOfMonth) {
	    LocalDate today = LocalDate.now();
	    LocalDate oldDate = LocalDate.of(year, month, dayOfMonth);
	    int p = (int)today.toEpochDay()-(int)oldDate.toEpochDay();
	    String data= "出生天数："+p;
	    return data;
	}
	
	
	//下个生日还有多少天
	public static String nextBirthday(int month,int day) {
		Calendar c = Calendar.getInstance();
		int year = c.get(Calendar.YEAR); 
		int nowmonth = c.get(Calendar.MONTH)+1; //方法返回值比实际月份小一
		int nowday = c.get(Calendar.DATE);
		int p ;
		String data= new String();;
		LocalDate today = LocalDate.now();
		if(month==nowmonth&&nowday==day)  
			data="你今天生日，生日快乐";
		
		if((nowmonth>month)||(nowmonth==month&&nowday>day)) {
			LocalDate newDate = LocalDate.of(year+1, month, day);
			p = (int)newDate.toEpochDay()-(int)today.toEpochDay();
			data= "还有"+p+"天生日";
			
			}
		if((nowmonth<month)||(nowmonth==month&&nowday<day)) {
			LocalDate newDate = LocalDate.of(year, month, day);
			p = (int)newDate.toEpochDay()-(int)today.toEpochDay();
			data="还有"+p+"天生日";
			}
		return data;
		
	}
	
	//查询星座
	
	public static String serXz(int month,int day) {
		String data=new String();
		if((month==2&&day>=19)||(month==3&&day<=20))
			data="你是双鱼座";
		if((month==1&&day>=20)||(month==2&&day<=18))
			data="你是水瓶座";
		if((month==12&&day>=22)||(month==1&&day<=19))
			data="你是魔蝎座";
		if((month==11&&day>=23)||(month==12&&day<=21))
			data="你是射手座";
		if((month==10&&day>=24)||(month==11&&day<=22))
			data="你是天蝎座";
		if((month==9&&day>=23)||(month==10&&day<=23))
			data="你是天枰座";
		if((month==8&&day>=23)||(month==9&&day<=29))
			data="你是处女座";
		if((month==7&&day>=23)||(month==8&&day<=22))
			data="你是狮子座";
		if((month==6&&day>=22)||(month==7&&day<=22))
			data="你是巨蟹座";
		if((month==5&&day>=21)||(month==6&&day<=21))
			data="你是双子座";
		if((month==4&&day>=20)||(month==5&&day<=20))
			data="你是金牛座";
		if((month==3&&day>=21)||(month==4&&day<=19))
			data="你是白羊座";
		
		return data;
	}
	
	//botpal添加功能按钮
	public void addButton(JButton button,ActionListener listener) {
		button.addActionListener(listener);
		botpal.add(button);
	}
	
	//下个生日  动作
	private class nextBirthday implements ActionListener{
		public void actionPerformed(ActionEvent event) {
			String data=new String();
			int month=Integer.valueOf((birmonth.getText()));
			int day=Integer.valueOf((birday.getText()));
			currectin(biryear.getText(),birmonth.getText(),birday.getText());
			if(currectin(biryear.getText(),birmonth.getText(),birday.getText())) {
				data="输入出生日期错误";
				result.setText(data);
				}
			else {
				data=nextBirthday(month,day);
				result.setText(data);
			}
			
		}
	}
	
	//出生天数 动作
	private class dayOfBirth implements ActionListener{
		public void actionPerformed(ActionEvent event) {
			String data=new String();
			int year=Integer.valueOf((biryear.getText()));
			int month=Integer.valueOf((birmonth.getText()));
			int day=Integer.valueOf((birday.getText()));
			if(currectin(biryear.getText(),birmonth.getText(),birday.getText())) {
				data="输入出生日期错误";
				result.setText(data);
				}
			else { 
				data=calculateTimeDifferenceByPeriod(year,month, day);
			result.setText(data);
			}
		}
	}
	
	//星座查询 动作
	private class serXz implements ActionListener{
		public void actionPerformed(ActionEvent event) {
			String data=new String();
			int month=Integer.valueOf((birmonth.getText()));
			int day=Integer.valueOf((birday.getText()));
			if(currectin(biryear.getText(),birmonth.getText(),birday.getText())) {
				data="输入出生日期错误";
				result.setText(data);
				}
			
			else {
				data=serXz(month,day);
				result.setText(data);
				}
			
		}
	}

	
}
