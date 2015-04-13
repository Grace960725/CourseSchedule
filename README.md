# CourseSchedule(in constructive way)
the second homework using java
import java.io.*;
import java.lang.String;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Scanner;
/*代码说明：
 *  课程表应用
建一个课程表:

星期四；三，四节；计算与软件工程；仙2-407；

通过命令行方式完成对课程的增、删、改、查、显示。

Add 星期四；三，四节；计算与软件工程；仙2-407；//如果成功 显示"已添加到文件中”

Remove 星期四；三，四节；计算与软件工程；仙2-407；//如果成功 显示"已从文件删除”

Update 星期四；三，四节；计算与软件工程；仙2-408；//如果成功 显示"已更新文件”

Find 星期四；三，四节； //如存在课程 显示 "课程名；上课地点”

Show //显示所有课程，按照时间排序

数据保存在文件里。

CurriculumSchedule.txt

假定：每周只有五天上课；每天只有上午一二三四节有课；且上课为两节连堂
 */
public class IOhelper{
	
	public static String file = "CurriculumSchedule.txt";
	
	public static void main (String[] args){
		IOhelper cl=new IOhelper();
		String course=cl.CourseInfor();
		System.out.println("原文件是："+course);
//读入指令
		System.out.println("请输入命令：（依照：“Add 星期四；三，四节；计算与软件工程；仙2-407；”的格式）");
		System.out.println("假定只有四节课");
		Scanner input=new Scanner(System.in);
		String Arith=input.next();
	    String courselist=input.nextLine().trim();
	    System.out.println("要进行的 算数操作是： "+Arith);
	    System.out.println("接收到的内容是："+courselist);
	    System.out.println("*************************************************");
	    System.out.println("*************************************************");
	    
	switch(Arith){
		//执行添加操作
	 case "Add":
		IOhelper add=new IOhelper();
		add.AddToFile(courselist);
		break;
    case "Remove":
	//执行删除操作
        IOhelper remove=new IOhelper();
		remove.RemoveFromFile(courselist);
		break;
    case "Update":
		//调用更新方法
		IOhelper update=new IOhelper();
	    update.UpdateFile(courselist);
	    break;
    case "Find":
	    //调用查询方法
	    IOhelper find=new IOhelper();
	    find.SearchFile(courselist);
	   break;
    case "Show":	
		//调用排序输出方法
		IOhelper sort=new IOhelper();
		sort.ShowFile();
		sort.printNew();
		break;
	  }
	}
	
	public static String CourseInfor(){
	       String result = "";
	         try{
	             BufferedReader br = new BufferedReader(new FileReader("CurriculumSchedule.txt"));//构造一个BufferedReader类来读取文件
	             String s = null;
	             while((s = br.readLine())!=null){//使用readLine方法，一次读一行
	                 result = result + "\n" +s;
	                 }
	             br.close();    
	         }catch(Exception e){
	             e.printStackTrace();
	         }
	         return result;
	     }
		
	//执行添加操作
	public void AddToFile(String courselist){
		String fileName="CurriculumSchedule.txt";
		String output=courselist;

		try{			
			FileWriter writer = new FileWriter(fileName,true);
			BufferedWriter bw=new BufferedWriter(writer);
			bw.write("\n"+output);
			bw.newLine();
         	bw.flush();//更新数据至源文件
			bw.close();
			System.out.println("已添加到文件中");
			}catch(IOException ex){
			ex.printStackTrace();
		}
	}
	
	//执行移除操作
	
  public void RemoveFromFile(String courselist){
	  int n=0;
	    String t1="";
            try {
            	BufferedReader br = new BufferedReader(new FileReader(file));//字符输入流化
                String t;
              while ((t = br.readLine()) != null) {
                 if(t.equals(courselist)==false&&n==0){
                	t1=t1+t;
                	n=1;
                 }
                 else if(t.equals(courselist)==false&&n==1){
                 	t1=t1+"\n"+t;
                  }
                 }	     
              BufferedWriter bw1=new BufferedWriter(new FileWriter(file));
              bw1.write(t1);
              bw1.close();
               
               br.close();
            } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
            
    }
	
	//执行更新操作
	public void UpdateFile(String courselist){
		char[] temp1=new char[10];
		char[] temp2=new char[10];
		int u=0;
		courselist.getChars(0, 8, temp2, 0);
		File file = new File("CurriculumSchedule.txt");

            try {
            	BufferedReader br0 = new BufferedReader(new FileReader(file));//字符输入流化
                String r1 ;
                String r2="";
                while ((r1 = br0.readLine()) != null) {//循环的读取一行一行读取文件，知道最后一行为空停止
                	r1.getChars(0, 8, temp1, 0);
                 if(temp1[2]==temp2[2]&&temp1[4]==temp2[4]){
                	r2 =r2+"\n"+courselist;  
                	  System.out.println("已成功替换");
                 }  
                 else if((temp1[2]==temp2[2]&&temp1[4]==temp2[4])==false&&u==0){
                    r2=r2+r1;
                    u=1;
                 }
                else if((temp1[2]==temp2[2]&&temp1[4]==temp2[4])==false&&u==1){
                     r2=r2+"/n"+r1;
                  }
	}
              
                BufferedWriter bw0 =new BufferedWriter(new FileWriter(file));
                bw0.write(r2);
                bw0.newLine();
                bw0.flush();//更新数据至源文件
                bw0.close();
           } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
    }
	
	//执行查找操作
	public void SearchFile(String courselist){
		char[] Label;
		Label=new char[15];
		
		File file = new File("CurriculumSchedule.txt");
		try {
            FileReader fr = new FileReader(file);//读取文件
            BufferedReader br = new BufferedReader(fr);//字符输入流化
            try {
                String s = new String();
                while ((s = br.readLine()) != null) {//循环的读取一行一行读取文件，知道最后一行为空停止
                 if(s.contains(courselist)){
                	System.out.println("该时段课程存在,信息如下：");
                	s.getChars(9, 24, Label, 0);
                	System.out.println(Label);
                 break;
                 }
                }
                
                br.close();//关闭输入流
                

            } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        } catch (FileNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
	
	//执行显示排序操作
	//根据星期几对每个string进行排序
	
	public void ShowFile(){
		String[] Label2;
		String[] Label3;
		Label2=new String[25];//存储排序前的课程信息
		Label3=new String[25];//用于存储排序后的课程信息
		int[] num;
		num=new int[20];
		
	    int i=0;
	    int j=0;
        int k=0;
        
		File file = new File("CurriculumSchedule.txt");
		try {
            FileReader fr = new FileReader(file);//读取文件
            BufferedReader br2 = new BufferedReader(fr);//字符输入流化
            try {
                String s,s3;
                while ((s = br2.readLine()) != null) {
                	Label2[i]=s;
                	if(s.contains("星期一；一，二节；"))
                		num[i]=11;
                	else if(s.contains("星期一；三，四节；"))
                		num[i]=12;
                	else if(s.contains("星期二；一，二节；"))
                		num[i]=21;
                	else if(s.contains("星期二；三，四节；"))
                		num[i]=22;
                	else if(s.contains("星期三；一，二节；"))
                		num[i]=31;
                	else if(s.contains("星期三；三，四节"))
                		num[i]=32;
                	else if(s.contains("星期四；一，二节"))
            		    num[i]=41;
                	else if(s.contains("星期四；三，四节"))
            		    num[i]=42;
            	    else if(s.contains("星期五；一，二节"))
            		    num[i]=51;
            	    else if(s.contains("星期五；三，四节"))
            		    num[i]=52;
                    i=i+1;
                }
                
                for(j=0;j<i;j++){
                	if(num[j]==11){
                		Label3[k]=Label2[j];
                	    k=k+1;
                	}
                }
                
                for(j=0;j<i;j++){
                	if(num[j]==12){
                		Label3[k]=Label2[j];
                	    k=k+1;
                	}
                }
                for(j=0;j<i;j++){
                	if(num[j]==21){
                		Label3[k]=Label2[j];
                	    k=k+1;
                }}
                for(j=0;j<i;j++){
                	if(num[j]==22){
                		Label3[k]=Label2[j];
                	    k=k+1;
                }
                }
                for(j=0;j<i;j++){
                	if(num[j]==31){
                		Label3[k]=Label2[j];
                	    k=k+1;
                }
                }
                for(j=0;j<i;j++){
                	if(num[j]==32){
                		Label3[k]=Label2[j];
                	    k=k+1;
                	}
                }
                for(j=0;j<i;j++){
                	if(num[j]==41){
                		Label3[k]=Label2[j];
                	    k=k+1;
                }
                }
                for(j=0;j<i;j++){
                	if(num[j]==42){
                		Label3[k]=Label2[j];
                	    k=k+1;
                }
                }
                for(j=0;j<i;j++){
                	if(num[j]==51){
                		Label3[k]=Label2[j];
                	    k=k+1;
                	}
                }
                for(j=0;j<i;j++){
                	if(num[j]==52){
                		Label3[k]=Label2[j];
                	    k=k+1;
                	}
                }
                //对课程时间进行排序，此处假定每次课只有两堂
                           
       System.out.println("更新后的数组是： ");
       FileWriter fw=new FileWriter("CurriculumSchedule.txt");
       BufferedWriter bw2 =new BufferedWriter(fw);
       for(int o=0;o<k;o++){
       s3=(String)Label3[o];
       System.out.println(s3);
       bw2.write(s3);
       bw2.newLine();
       }
       bw2.close();                                      	            
       } catch (IOException e) {
         // TODO Auto-generated catch block
           e.printStackTrace();
            }
        } catch (FileNotFoundException e) {
       // TODO Auto-generated catch block
        e.printStackTrace();
       }
       } 
		
	//验证是否正确添加
	public void printNew(){
		System.out.println("更新后的文件是：");
		File file = new File("CurriculumSchedule.txt");//获得文件
        try {
            FileReader fr = new FileReader(file);//读取文件
            BufferedReader br = new BufferedReader(fr);//字符输入流化
            try {
                String f1 = new String();
                String f2="";
                while ((f1 = br.readLine()) != null) {//循环的读取一行一行读取文件，知道最后一行为空停止
                 f2 += f1 + "\n ";
                }
                br.close();//关闭输入流
                System.out.println(f2);//打印输出TXT文件中的数据

            } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        } catch (FileNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
	}
