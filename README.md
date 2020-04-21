# JDBC_Project-201658034--
데이타베이스프로그래밍 1차과제 코드

package com.hanshin.database;

import java.sql.Statement;
import java.util.Scanner;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class ex {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		String jdbc_driver = "com.mysql.cj.jdbc.Driver";
		String jdbc_url = "jdbc:mysql://localhost:3306/workbench?characterEncoding=UTF-8&serverTimezone=UTC";
		try {
			; //table name
			Class.forName(jdbc_driver);
			System.out.println("JDBC_Driver connection Success");
			Connection con = DriverManager.getConnection(jdbc_url, "root", "suhyeon1250*");
			Statement st = (Statement) con.createStatement();
			st.executeUpdate(
					"CREATE TABLE addressbook ( id INT, name VARCHAR(45), tel VARCHAR(45), email VARCHAR(60), address VARCHAR(60))");
			System.out.printf("Create Table Success\n");

			ResultSet rs = ((java.sql.Statement) st).executeQuery("select * from addressbook");

			
			String sql = "insert into addressbook (id,name,tel,email,address) values(?,?,?,?,?)";
			PreparedStatement pstmt = con.prepareStatement(sql);
			
			int id[] = { 1, 2, 3, 4, 5 };
			String name[] = { "최수현 ", "나진영 ", "조필상 ", "김상섭 ", "장원석 " };
			String tel[] = { "01040100447", "01034512257", "01030351276", "01028572411", "01045232814" };
			String email[] = { "suhyeon1137", "nage1", "jophi6", "ghimsan", "jangwon" };
			String address[] = { "경기도 화성", "경기도 용인", "경기도 시흥", "경기도 안산", "경기도 수원" };

			for (int i = 0; i < 5; i++) {
				pstmt.setInt(1, id[i]);
				pstmt.setString(2, name[i]);
				pstmt.setString(3, tel[i]);
				pstmt.setString(4, email[i]);
				pstmt.setString(5, address[i]);
				pstmt.executeUpdate();
				
			} 
			System.out.println("insert success");

			rs = ((java.sql.Statement) st).executeQuery("select * from addressbook");
			while (rs.next()) {
				int id1 = rs.getInt("id");
				String name1 = rs.getString("name");
				String tel1 = rs.getString("tel");
				String email1 = rs.getString("email");
				String address1 = rs.getString("address");

				System.out.printf("id: %d ,", id1);
				System.out.printf("name: %s ,", name1);
				System.out.printf("tel: %s ,", tel1);
				System.out.printf("email: %s ,", email1);
				System.out.printf("address: %s \n", address1);
			}
			System.out.println("first clear");
			
			
		    pstmt = con.prepareStatement("UPDATE addressbook SET email =?");
		    
		    for(int i=1; i<5; i++) {
		    	pstmt.setString(1, email[i]+"@naver.com");
		    	pstmt.executeUpdate();
		    }
			
		    
			rs = ((java.sql.Statement) st).executeQuery("select * from addressbook");
			while (rs.next()) {
				int id1 = rs.getInt("id");
				String name1 = rs.getString("name");
				String tel1 = rs.getString("tel");
				String email1 = rs.getString("email");
				String address1 = rs.getString("address");

				System.out.printf("id: %d ,", id1);
				System.out.printf("name: %s ,", name1);
				System.out.printf("tel: %s ,", tel1);
				System.out.printf("email: %s ,", email1);
				System.out.printf("address: %s \n", address1);
			}
			System.out.println("two clear");
			
			st.executeUpdate("DELETE FROM addressbook WHERE id = '4'");
			st.executeUpdate("DELETE FROM addressbook WHERE id = '5'");
			rs = ((java.sql.Statement) st).executeQuery("select * from addressbook");
			while (rs.next()) {
				int id1 = rs.getInt("id");
				String name1 = rs.getString("name");
				String tel1 = rs.getString("tel");
				String email1 = rs.getString("email");
				String address1 = rs.getString("address");

				System.out.printf("id: %d ,", id1);
				System.out.printf("name: %s ,", name1);
				System.out.printf("tel: %s ,", tel1);
				System.out.printf("email: %s ,", email1);
				System.out.printf("address: %s \n", address1);
				
			}
			System.out.println("three clear");
				rs.close();
			st.close();
			con.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
