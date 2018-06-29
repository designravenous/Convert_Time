# Convert_Time
C# application to convert specific time to different timezones. Console application


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace The_Time
{
    class Program
    {public class Time
        {
            public int year;
            public int month;
            public int day;
            public int hour;
            public int min;
            public int second;
            

            public void dateMethod()
            {
                Console.WriteLine("\t{0}/{1}/{2} {3}:{4}:{5}:", year,month,day,hour,min,second);
            }
            public void gmtMethod()
            {
                Console.WriteLine("\t{0}/{1}/{2} {3}:{4}:{5}:", year, month, day, --hour, min, second);
            }
           public Time (System.DateTime dt)
            {
                year = dt.Year;
                month = dt.Month;
                day = dt.Day;
                hour = dt.Hour;
                min = dt.Minute;
                second = dt.Second;
                
                
            }
            public int theHour
            {
                get { return hour; }
                set { value = hour; }
            }
        }
        
        static void Main(string[] args)
        {
            DateTime currentTime = System.DateTime.Now;
            Time date = new Time(currentTime);

            Console.WriteLine("\n\tCET DATE/HOUR:");
            date.dateMethod();
            Console.WriteLine("\n\tGMT & UTC DATE/HOUR:");
            date.gmtMethod();

            currentTime = currentTime.AddHours(-6); // ger currentTime nutidsvärde -6
            Time afterSixHours = new Time(currentTime); //ny konstruktor
            Console.WriteLine("\n\tEST DATE/HOUR:");
            afterSixHours.dateMethod();

            currentTime = currentTime.AddHours(6); //ger rätt värde till currentTime
            currentTime = currentTime.AddHours(-9); // för att sedan sänka den med 9 timmar
            Console.WriteLine("\n\tPST DATE/HOUR:");
            Time afterNineHours = new Time(currentTime); // ny konstruktor för PST
            afterNineHours.dateMethod();

            //After showing the current REALTIME convertions
            Console.Write("\n\tWould you like to convert a specifik UTC/GMT/EST/PST time to CET? (Y/N)\t");
            string userAnsw = Console.ReadLine();

            if (userAnsw == "Y" || userAnsw == "y")
            {
                Console.Write("\tEnter the Timezone you want to convert to CET: ");
                string timeZone = Console.ReadLine();

                switch (timeZone)
                {
                    case "GMT":
                        Console.Write("\tWrite in the Time in GMT/UTC to get CET (format Month/Day/Year Hour:min:second):");
                        string iDate = Console.ReadLine();

                        DateTime oFate = Convert.ToDateTime(iDate);
                        DateTime cetFromGMT = oFate.AddHours(1);
                        Console.WriteLine("\n\n\t" + cetFromGMT.Year + "/" + cetFromGMT.Month + "/" + cetFromGMT.Day + "\t" + cetFromGMT.Hour + ":" + cetFromGMT.Minute + ":" + cetFromGMT.Second);
                        Console.ReadKey();
                        break;
                    case "gmt":
                        goto case "GMT";
                    case "UTC":
                        goto case "GMT";
                    case "utc":
                        goto case "GMT";
                    case "EST":
                        Console.Write("\tWrite in the Time in EST to get CET (format Month/Day/Year Hour:min:second):");
                        string estZone = Console.ReadLine();

                        DateTime myFate = Convert.ToDateTime(estZone);
                        DateTime cetFromEST = myFate.AddHours(6);
                        Console.WriteLine("\n\n\t"+cetFromEST.Year + "/" + cetFromEST.Month + "/" + cetFromEST.Day + "\t" + cetFromEST.Hour + ":" + cetFromEST.Minute + ":" + cetFromEST.Second);
                        Console.ReadKey();
                        break;
                    case "est":
                        goto case "EST";
                    case "PST":
                        Console.Write("\tWrite in the Time in PST to get CET (format Month/Day/Year Hour:min:second):");
                        string pstZone = Console.ReadLine();

                        DateTime estFate = Convert.ToDateTime(pstZone);
                        DateTime estTocet = estFate.AddHours(9);
                        Console.WriteLine("\n\n\t" + estTocet.Year + "/" + estTocet.Month + "/" + estTocet.Day + "\t" + estTocet.Hour + ":" + estTocet.Minute + ":" + estTocet.Second);
                        Console.ReadKey();
                        break;
                    case "pst":
                        goto case "PST";

                    default:
                        Console.WriteLine("Incorrect Time Zone");
                        break;

                }
            }
            Console.Write("\tExeting Program Y/N: "); 
            string exit = Console.ReadLine();
            if (exit == "y" || exit == "Y") { 
            Environment.Exit(0);
            }

            Console.ReadKey();

        }
    }
}
