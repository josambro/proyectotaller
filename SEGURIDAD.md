proyectotaller
==============

modulo de seguridad
//Jose Alejandro Ambrosio
//Modulo iniciar sesion 
//version 1.0
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace EBRICENTER
{
    public partial class wfIniciarSesion : Form
    {
        string sUsuario;

        public wfIniciarSesion()
        {
            InitializeComponent();
        }

        private void btnSalir_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void btnIniciarSesion_Click(object sender, EventArgs e)
        {

            MySqlConnection  obCon = new MySqlConnection("server=localhost; User Id=root; Pwd=151088; database=login");
            //En donde server="nombre del servidor", user id="root" Pwd=contaseña y database="Nombre de la BD a la que nos conectaremos.
           
            obCon.Open(); //Abrimos la conexion creada.
            MySqlCommand obCmd = new MySqlCommand("SELECT username,password,id_extreme FROM usuarios WHERE username='" + txtUsuario.Text + "'AND password='" + txtContrasena.Text + "' ", con); //Realizamos una selecion de la tabla usuarios.
            MySqlDataReader leer = obCmd.ExecuteReader();



            string sCodigo = null;


    
            if (leer.Read()) //Si el usuario es correcto nos abrira la otra ventana.
            {
                sCodigo = leer.GetString("id_extreme");
                if (sCodigo.Equals("1") == true)
                {
                    MessageBox.Show("Bienvenido al sistema " + txtUsuario.Text);
                    sUsuario = txtUsuario.Text;
                    btnprodu MenuPrincipal = new btnprodu(sUsuario);
                    MenuPrincipal.Show();
                   // MenuPrincipal.tsslEstado.Text = "Conectado - "+sUsuario;
                    this.Hide();

                }
                if (sCodigo.Equals("2") == true)
                {
                    MessageBox.Show("Bienvenido " + txtUsuario.Text);
                    sUsuario = txtUsuario.Text;
                    wfClientes MenuPrincipal = new wfClientes();
                    MenuPrincipal.Show();
                    //MenuPrincipal.tsslEstado.Text = "Conectado - "+sUsuario;
                    this.Hide();

                }
            }

                
                else //Si no lo es mostrara este mensaje.
                MessageBox.Show("Error - Ingrese sus datos correctamente");
                obCon.Close(); //Cerramos la conexion.
           
   
        }

        private void txtUsuario_TextChanged(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {

        }

        private void wfIniciarSesion_Load(object sender, EventArgs e)
        {

        }

        private void pboLogo_Click(object sender, EventArgs e)
        {

        }
    }
}
