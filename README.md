# jdbcselect-program
jdbc select code
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.PreparedStatement;
import java.sql.CallableStatement;


public class JdbcConnect{
	
	public static void main(String[] args) {
		Connection conn=null;
		Statement st=null;
		ResultSet rs=null;
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			conn=DriverManager.getConnection("jdbc:mysql://localhost:3306/firstsql",
					"root","root");
			if(conn!=null) {
				st=conn.createStatement();
				String query="select * from emp";
				
				if(st!=null) {
					rs=st.executeQuery(query);
				}
			}
			if(rs!=null) {
				boolean isEmptyRs=true;
				while(rs.next()) {
					isEmptyRs=false;
					System.out.println(rs.getInt(1)+" "+rs.getString(2));
					System.out.println(rs.getInt("empno")+" "+rs.getString("ename"));
				}
				if(isEmptyRs) {
					System.out.println("records not found");
				}
				else {
					System.out.println("records  found");
				}
			}
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			try {
				if(conn!=null)
					conn.close();
				if(st!=null)
					st.close();
				if(rs!=null)
					rs.close();
			}catch(SQLException e) {
				e.printStackTrace();
			}
	}
}
}
