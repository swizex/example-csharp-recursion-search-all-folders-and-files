```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;
using System.Text;
using System.Threading.Tasks;

namespace SimpleSearchEngineCMDedition
{
    class Program
    {
        static void Main(string[] args)
        {

            Console.WriteLine("Please insert the correct root path you wish to search in\n");
            string _path = Console.ReadLine();
            Console.WriteLine("Please insert the correct folder name you wish to search in\n");
            string _filename = Console.ReadLine();
            Console.WriteLine("Searching...\n");

            Console.WriteLine("\n");//additional spaces for new cmd layout

            List<string> _result = new List<string>();//this list will hold all found directories/files

            _result = _Search(_path, _filename);

            Console.WriteLine("\n");//additional spaces for new cmd layout
           
            Console.WriteLine("Enter quit to exit program...");

            string _input = Console.ReadLine();

            if(_input == "quit")
            {
                System.Environment.ExitCode = 0;
            }
        }

        public static List<string> _Search(string _filepath,string _filename)
        {
            //creating a temp list to store all found directories/files...
            List<string> _templist = new List<string>();


            string[] filelist = Directory.GetFiles(_filepath + _filename);


            int i = 0;//counter

            Console.WriteLine("Found Files in " + _filename + "\n");

            foreach (string lfile in filelist)
            {
                

                if (lfile == filelist[i])
                {
                    
                    Console.WriteLine(filelist[i]);

                }

                i++;
            }

            Console.WriteLine("\n");

            string[] _Directorylist = Directory.GetDirectories(_filepath + _filename);

            foreach (string lDirectory in _Directorylist)
            {
                _templist.Add(lDirectory);

                _templist.AddRange(_Search(_filepath + _filename, lDirectory.Remove(0, lDirectory.LastIndexOf('\\'))));//recursion...
                
            }

            
            return _templist;

        }
    }
}

//programmed by Teddy Morduhovich, 2018.
```
