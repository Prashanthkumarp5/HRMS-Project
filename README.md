# HRMS-Project
    package hrms.DataConnection;

    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    import javax.swing.JOptionPane;

    public class ConnectionClass {

    private static final String URL = "jdbc:mysql://localhost:3306/gms";
    private static final String USER_NAME = "root";
    private static final String PASSWORD = "";
    private static Connection connection = null;
    private static Statement statement = null;

    /* Creating Connection*/
    public static void connection(){
       try{
           Class.forName("com.mysql.jdbc.Driver");
            connection = DriverManager.getConnection(URL, USER_NAME, PASSWORD);
            statement = connection.createStatement();
            System.out.println("Connection Opened");
        }catch(SQLException e){            
            JOptionPane.showMessageDialog(null, "Connection is not Opened ! " + e.getMessage());      
        }catch(Exception e){
        }
    }
    /*  Selecting Query */
    public static ResultSet selectQuery(String query) {
        try{
            return statement.executeQuery(query);
        }catch(SQLException e){
            e.getMessage();
            return null;
            
        }
    }
    /*  Executing Query */
    public static boolean query(String query) {
        try{
            return statement.execute(query);
        }catch(SQLException e){
            e.getMessage();
            throw new IllegalArgumentException();
        }
    }
    /* Prepares the data first then execute it */
     public static PreparedStatement getPreStatement(String query)
     {
       try {
           return statement.getConnection().prepareStatement(query);
         } catch (SQLException e) {}
       return null;
     }
    }
