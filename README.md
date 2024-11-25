using System;
using System.Windows.Forms;
using EnrolmentSystem;
using jeanEnrollmentSystem;

public partial class frmStudent : Form
    {
        String connString;
        private TextBox txtStudentIdNumber;
        private Textbox txtFirstName;
        private TextBox txtLastName;
        private Textbox txtGender;
        private Textbox txtAge;

        public frmStudent()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            throw new NotImplementedException();
        }

        private void frmStudent_Load(object sender, EventArgs e)
        {

        }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            try
            {
                connString = "server=localhost; database=tongcuadbdb; Uid=root; pwd=admin;";

                string query = "insert into tblStudent(StudentIdNumber,LastName,FirstName,Age,Gender) values('" + txtStudentIdNumber.Text + "','" + txtLastName.Text + "','" + txtFirstName.Text + "','" + txtAge.Text + "','" + txtGender.Text + "')";

                MySqlConnection conn = new MySqlConnection(connString);
                MySqlCommand cmd = new MySqlCommand(query, conn);
                MySqlDataReader myReader;
                conn.Open();
                myReader = cmd.ExecuteReader();

                MessageBox.Show("Record insert to the Database Successfully");

                txtStudentIdNumber.Clear();
                txtLastName.Clear();
                txtFirstName.Clear();
                txtAge.Clear();
                txtGender.Clear();

                myReader.Close();
                conn.Close();

            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void btnSearch_Click(object sender, EventArgs e)
        {
            try
            {
                connString = "server==localhost; database=tongcuadb; Uid=root; pwd=admin;";

                string query = "select * from tblStudent where StudentIdNumber='" + txtStudentIdNumber + "'";

                MySqlConnection conn = new MySqlConnection(connString);
                MySqlCommand cmd = new MySqlCommand(query, conn);
                MySqlDataReader myReader;
                conn.Open();
                myReader = cmd.ExecuteReader();
                if (myReader.Read())
                {

                    MessageBox.Show("Record Found!" + "Welcome " + myReader.GetString("lastname") + ", " + myReader.GetString("firstname") + "," + myReader.GetString("Age") + "," + myReader.GetString("Gender"));

                    txtFirstName.Text = myReader.GetString("firstName");
                    txtLastName.Text = myReader.GetString("lastName");
                    txtAge.Text = myReader.GetString("Age");
                    txtGender.Text = myReader.GetString("Gender");
                }
                myReader.Close();
                conn.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void btnUpdate_Click(object sender, EventArgs e)
        {
            try
            {
                connString = "server=localhost; database = tongcuadb;Uid=root;";

                string query = "update tblStudent set firstname='" + txtFirstName.Text + "', lastname='" + txtLastName.Text + "',Age='" + txtAge.Text + "' Gender='" + txtGender + "' where id='" + txtStudentIdNumber.Text + "'";
                MySqlConnection conn = new MySqlConnection(connString);
                MySqlCommand cmd = new MySqlCommand(query, conn);
                MySqlDataReader myReader;
                conn.Open();
                myReader = cmd.ExecuteReader();
                myReader.Close();
                conn.Close();

                txtStudentIdNumber.Clear();
                txtLastName.Clear();
                txtFirstName.Clear();
                txtAge.Clear();
                txtGender.Clear();

                MessageBox.Show("Update Record Done");
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void btnDelete_Click(object sender, EventArgs e)
        {
            try
            {
                connString = "server=localhost; database = tongcuadb;Uid=root;";

                string query = "delete from tblStudent where id='" + txtStudentIdNumber.Text + "'";

                MySqlConnection conn = new MySqlConnection(connString);
                MySqlCommand cmd = new MySqlCommand(query, conn);
                MySqlDataReader myReader;
                conn.Open();
                myReader = cmd.ExecuteReader();
                myReader.Close();
                conn.Close();

                txtStudentIdNumber.Clear();
                txtLastName.Clear();
                txtFirstName.Clear();
                txtAge.Clear();
                txtGender.Clear();

                MessageBox.Show("Delete Record Done!");
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }
    }
