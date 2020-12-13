using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.SpeechRecognitionEngine;



namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        SpeechRecognitionEngine recoengine = new SpeechRecognitionEngine();
        bool izin;
        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void pictureBox1_Click(object sender, EventArgs e)
        {
            pictureBox1.Visible = false;
            sestanima_ayarlari();
            izin = true;
            recoengine.RecognizeAsync();
        }

        void sestanima_ayarlari()
        {
            string[] ihtimaller = { "Hello", " Thank you", " Please open valorant" };
            Choices seçenekler = new Choices(ihtimaller);
            Grammar grammer = new Grammar(new GrammarBuilder(seçenekler));
            recoengine.LoadGrammar(grammer);
            recoengine.SetInputToDefaultAudioDevice();
            recoengine.SpeechRecognized += ses_tanıdığında;
        }
        private void ses_tanıdığında (object sender, SpeechRecognizedEventArgs e04)
        {
            if (izin == true)
            {
                pictureBox1.Visible = true;
                izin = false;
                if(e04.Result.Text =="Please open valorant")
                {
                    System.Diagnostics.Process.Start("C://Riot Games//VALORANT//VALORANT");
                }
            }
        }
    }
}
