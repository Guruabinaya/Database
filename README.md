# Database
import java.util.*;
import java.sql.*;

public class MoviesDB {

	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		System.out.println("If go to choice press 1");   //view choices
		int ch=sc.nextInt();
		if(ch==1) {  //  enter 1->go to choices
			choice();
		}
		else {   //else exit
	       System.out.println("Exit");
	    }
		sc.close();
    }

	static void choice() {
		Scanner sc=new Scanner(System.in);
		System.out.print("The Choice Are: 1.CreateDatabase  2.CreateTable  3.InsertDatabase  4.ViewDatabase  5.Exit");
		System.out.println();
		System.out.print("Enter Choice: ");   
		int choice=sc.nextInt();
		switch(choice) {
		  
		   case 1:
		   {
			   try {
					String driver="com.mysql.cj.jdbc.Driver";
					String databaseurl="jdbc:mysql://localhost:3306"; //DBConnectivity
					String username="root";
					String password="";
					Class.forName(driver);
					Connection conn=DriverManager.getConnection(databaseurl,username,password);
					Statement stmt = conn.createStatement();
					String res = "CREATE DATABASE moviesDB";  //create database ->moviesDB
			        stmt.executeUpdate(res);
			        System.out.println("Database Created");
			        System.out.println();
			        System.out.println("IF YOU WANT TO CONTINUE?(1/0)"); //if continue press 1 else 0
			        int a=sc.nextInt();
			        if(a==1) {
			        	choice();
			        }
			        else {
			        	System.out.println("Exit");
			        }
			        
				}
				catch(Exception e) {
					System.out.println(e);
				}
			    break;
		   }
		   
		   case 2:
		   {
			   try
			   {
			    String driver="com.mysql.cj.jdbc.Driver";
				String databaseurl="jdbc:mysql://localhost:3306/moviesDB";
				String username="root";
				String password="";
				Class.forName(driver);
				Connection conn=DriverManager.getConnection(databaseurl,username,password);
				Statement stmt = conn.createStatement();
				String res="CREATE TABLE movies " +         //create table ->movies
		                   "(moviename VARCHAR(20) not NULL, " +
		                   " actor VARCHAR(25), " + 
		                   " actress VARCHAR(25), " + 
		                   " releaseyear VARCHAR(5), " + 
		                   " director VARCHAR(25), " +                       
		                   " PRIMARY KEY ( moviename ))";
				stmt.executeUpdate(res);
				System.out.println("Created table in database");
				System.out.println();
				System.out.println("IF YOU WANT TO CONTINUE?(1/0)");
				int a=sc.nextInt();
		        if(a==1) {
		        	choice();
		        }
		        else {
		        	System.out.println("Exit");
		        }
			   }
			   catch(Exception e) {
				   System.out.println(e);
			   }
			   break;
		   }
		   
		   case 3:
		   {
			   try {
					String driver="com.mysql.cj.jdbc.Driver";
					String databaseurl="jdbc:mysql://localhost:3306/moviesDB";
					String username="root";
					String password="";
					Class.forName(driver);
					Connection conn=DriverManager.getConnection(databaseurl,username,password);
					
					Scanner sc1=new Scanner(System.in);
					
					System.out.print("Enter MovieName: ");
					String name=sc1.next();
					System.out.print("Enter ActorName: ");
					String actor=sc1.next();
					System.out.print("Enter ActressName: ");
					String actress=sc1.next();
					System.out.print("Enter year: ");      //get input from user and store database
					String year=sc1.next();
					System.out.print("Enter DirectorName: ");
					String director=sc1.next();
					System.out.println();                         //insert database in table
					String res="INSERT INTO movies(Moviename,Actor,Actress,Releaseyear,Director) VALUES ('"+name+"', '"+actor+"', '"+actress+"', '"+year+"', '"+director+"')";
					Statement stmt = conn.createStatement();       //like("pattas","dhanush","sneha","2020","ranjith")
					stmt.executeUpdate(res);
					System.out.println("Inserted Successfully"); 
					System.out.println();
					System.out.println("IF YOU WANT TO CONTINUE?(1/0)");
					int a=sc.nextInt();
			        if(a==1) {
			        	choice();
			        }
			        else {
			        	System.out.println("Exit");
			        }
			        sc1.close();
				}
				catch(Exception e){
					System.out.println(e);
				}
			   break;
		   }
		   
		   case 4:
		   {
			   try
			   {
			    String driver="com.mysql.cj.jdbc.Driver";
				String databaseurl="jdbc:mysql://localhost:3306/moviesDB";
				String username="root";
				String password="";
				Class.forName(driver);
				Connection conn=DriverManager.getConnection(databaseurl,username,password);
				Statement stmt = conn.createStatement(); 
				ResultSet rs = stmt.executeQuery("SELECT * FROM movies");  //to view table
		        System.out.println("moviename  actor  actress  releaseyear  director");
		        while (rs.next()) {
		            String name = rs.getString("moviename");
		            String actor = rs.getString("actor");
		            String actress = rs.getString("actress");
		            String releaseyear = rs.getString("releaseyear");
		            String director = rs.getString("director");
		            System.out.println(name+"  "+actor+"  "+actress+"  "+releaseyear+"  "+director);
		           }
		            System.out.println();
		            System.out.println("IF YOU WANT TO CONTINUE?(1/0)");
		            int a=sc.nextInt();
			        if(a==1) {
			        	choice();
			        }
			        else {
			        	System.out.println("Exit");
			        }
		       }
			   catch(Exception e) {
				   System.out.println(e);
			   }
			   break;
		   }
		   
		   case 5:
		   {
			   System.out.println("EXIT");  //exit
			   break;
		   }
	   }
	  sc.close();
}
		
}	
