using System;
using static System.Console;
using System.Globalization;
class GreenvilleRevenue
{
    static void Main()
    {
//set variables and arrays
        const int MIN_CONTESTANTS = 0;
        const int MAX_CONTESTANTS = 30;
        int num;
        int revenue = 0;
        Contestant[] contestants = new Contestant[MAX_CONTESTANTS];
  //gets info from classes
        num = getContestantNumber(MIN_CONTESTANTS, MAX_CONTESTANTS);
        revenue = getContestantData(num, contestants, revenue);
        WriteLine("\n\nRevenue expected this year is {0}", revenue.ToString("C", CultureInfo.GetCultureInfo("en-US")));
        getLists(num, contestants);
    }
    private static int getContestantNumber(int min, int max)
    {
  //user inputs number between 0-30,if not it will ask again,converted to INT
        string entryString;
        int num = max + 1;
        Write("Enter number of contestants >> ");
        entryString = ReadLine();
        while (num < min || num > max)
        {
            if (!int.TryParse(entryString, out num))
            {
                WriteLine("Format invalid");
                num = max + 1;
                Write("Enter number of contestants >> ");
                entryString = ReadLine();
            }
            else
            {
//user inputs number between 0-30,if not it will ask again,converted to INT
                if (num < min || num > max)
                {
                    WriteLine("Number must be between {0} and {1}", min, max);
                    num = max + 1;
                    Write("Enter number of contestants >> ");
                    entryString = ReadLine();
                }
            }
        }
        return num;
    }
    private static int getContestantData(int num, Contestant[] contestants, int revenue)
    {
  //set variables
        const int ADULTAGE = 17;
        const int TEENAGE = 12;
        int x = 0;
        string name;
        char talent;
        int age;
  //userinputs name,stored in an array with accordin talent 
        while (x < num)
        {
            Write("Enter contestant name >> ");
            name = ReadLine();
            WriteLine("Talent codes are:");
            for (int y = 0; y < Contestant.talentCodes.Length; ++y)
                WriteLine("  {0}   {1}", Contestant.talentCodes[y], Contestant.talentStrings[y]);
    //stores talent in array
            Write("       Enter talent code >> ");
            char.TryParse(ReadLine(), out talent);
            Write("       Enter contestant's age >> ");
    //stores age in array
            int.TryParse(ReadLine(), out age);
 //checkin the age of contestant
            if (age > ADULTAGE)
                contestants[x] = new AdultContestant();
            else
               if (age > TEENAGE)
                contestants[x] = new TeenContestant();
            else
                contestants[x] = new ChildContestant();
            contestants[x].Name = name;
            contestants[x].TalentCode = talent;
            revenue += contestants[x].Fee;
            ++x;
        }

        return revenue;
  //returns to display
    }
    private static void getLists(int num, Contestant[] contestants)
    {
//set variables
        int x;
        char QUIT = 'Z';
        char option;
        bool isValid;
        int pos = 0;
        bool found;
//user inputs code to see whos in that talent or Z to end the program 
        WriteLine("\nThe types of talent are:");
        for (x = 0; x < Contestant.talentStrings.Length; ++x)
            WriteLine("{0, -6}{1, -20}", Contestant.talentCodes[x], Contestant.talentStrings[x]);
        Write("\nEnter a talent type or {0} to quit >> ", QUIT);
        isValid = false;
        while (!isValid)
        {
  //if user enter anything besides the talents or Z
            if (!char.TryParse(ReadLine(), out option))
            {
                isValid = false;
                WriteLine("Invalid format - entry must be a single character");
                Write("\nEnter a talent type or {0} to quit >> ", QUIT);
            }
            else
            {
                if (option == QUIT)
                    isValid = true;
                else
                {
  //Displays the talent and name associated with it
                    for (int z = 0; z < Contestant.talentCodes.Length; ++z)
                    {
                        if (option == Contestant.talentCodes[z])
                        {
                            isValid = true;
                            pos = z;
                        }
                    }
                    if (!isValid)
                    {
  //if user enter anything besides the talents or Z
                        WriteLine("{0} is not a valid code", option);
                        Write("\nEnter a talent type or {0} to quit >> ", QUIT);
                    }
                    else
                    {
    //Displays the talent and name associated with it
                        WriteLine("\nContestants with talent {0} are:", Contestant.talentStrings[pos]);
                        found = false;
                        for (x = 0; x < num; ++x)
                        {
                            if (contestants[x].TalentCode == option)
                            {
                                WriteLine(contestants[x].ToString());
                                found = true;
                            }
                        }
  //if talents have no contestant

                        if (!found)
                            WriteLine("No contestants had talent {0}", Contestant.talentStrings[pos]);
                        isValid = false;
                        Write("\nEnter a talent type or {0} to quit >> ", QUIT);
                    }
                }
            }
        }
    }
}
public class Contestant
{
 //set variables and arrays
    public static char[] talentCodes = { 'S', 'D', 'M', 'O' };
    public static string[] talentStrings = {"Singing", "Dancing",
           "Musical instrument", "Other"};
//get set method to get name
    public string Name { get; set; }
    public char talentCode;
    public string talent;
 //get set method to get talentCode
    public char TalentCode
    {
        get
        {
            return talentCode;
        }
        set
        {
  //if user enter anything besides the talents or Z
            int pos = talentCodes.Length;
            for (int x = 0; x < talentCodes.Length; ++x)
                if (value == talentCodes[x])
                    pos = x;
            if (pos == talentCodes.Length)
            {
                talentCode = 'I';
                talent = "Invalid";
            }
            else
            {
                talentCode = value;
                talent = talentStrings[pos];
            }
        }

    }
    public string Talent
    {
        get
        {
            return talent;
        }
    }
//get set method to get Fee
    public int Fee { get; set; }
}
//subclass of Contestant
public class AdultContestant : Contestant
{
  //set variable
    public int ADULT_FEE = 30;
  //constructor 
    public AdultContestant()
    {
        Fee = ADULT_FEE;
    }
  //override string to display adult fee
    public override string ToString()
    {
        return ("Adult Contestant " + Name + " " + TalentCode + "   Fee " + Fee.ToString("C", CultureInfo.GetCultureInfo("en-US")));
    }
}
//subclass of Contestant
public class TeenContestant : Contestant
{
//set variable
    public int TEEN_FEE = 20;
 //Constructor
    public TeenContestant()
    {
        Fee = TEEN_FEE;
    }
//override string to display Teen fee
    public override string ToString()
    {
        return ("Teen Contestant " + Name + " " + TalentCode + "   Fee " + Fee.ToString("C", CultureInfo.GetCultureInfo("en-US")));
    }
}
//subclass of Contestant
public class ChildContestant : Contestant
{
//set variable
    public int CHILD_FEE = 15;
//Constructor
    public ChildContestant()
    {
        Fee = CHILD_FEE;
    }
//override string to display Child fee
    public override string ToString()
    {
        return ("Child Contestant " + Name + " " + TalentCode + "   Fee " + Fee.ToString("C", CultureInfo.GetCultureInfo("en-US")));
    }
}
