using System.IO;
using System;

class Program
{
    public static int MyPosition = 0;
    static void Main()
    {
        ConsoleKeyInfo Key;
        string[] SysDrives = UserGetDrives(); // Список имен Томов
        string[] NowDir = SysDrives; // список имен Каталогов
        string path = null; //Выбранный Каталог\Том
        UpdateScr(SysDrives); //первое обналение Экрана Консоли
        //main program body (Цикл Обработки Действий)       
        while (true)
        {
            Key = Console.ReadKey();
            if (Key.Key == ConsoleKey.Enter)
            {                
                path = NowDir[MyPosition]; //новый путь
                NowDir = UserGetDir(path); //Получение списка ПодКаталогов текущего каталога/Тома 
                MyPosition = 0;
            }
            //возвращение к предидущему по иерархии каталогу(Шаг назад)
            if (Key.Key == ConsoleKey.Escape)
            {
                try
                {
                    path = Directory.GetParent(path).Name;
                    NowDir = UserGetDir(path);
                }
                //на случай если не удалось перейти к родительскому каталогу
                catch 
                { 
                    NowDir = SysDrives;
                }
                
            }
            else
            {
                MovePosition(Key); // обработка нажатий UpArrow и DownArrow
            }
            UpdateScr(NowDir); //Обновлеие Экрана Консоли
        }
    }

    //получение Всех Томов
    static string[] UserGetDrives()
    {
        DriveInfo[] drives = DriveInfo.GetDrives();
        int i = 0;
        string[] DRIVE = new string[drives.Length];
        foreach (DriveInfo drive in drives)
        {
            DRIVE[i] = drive.Name + @"\";
            i += 1;            
        }
        return DRIVE;
    }

    //Получение Каталогов по указанной ссылке
    static string[] UserGetDir(string dirName)
    {        
        if (Directory.Exists(dirName))
        {
             return Directory.GetDirectories(dirName);
        }
        else
        {
            return UserGetDrives();
        }
    }

    // обработка нажатий UpArrow и DownArrow
    static void MovePosition(ConsoleKeyInfo key)
    {
        if (key.Key == ConsoleKey.UpArrow)
        {
            if(MyPosition > 0)
            {
                MyPosition -=1;
            }
            else
            {
                MyPosition = 0;
            }
        }
        if (key.Key == ConsoleKey.DownArrow)
        {
            MyPosition += 1;
        }
    }

    //АпдейтСкрин - итс АпдейтСкрин, андерстэнд?
    static void UpdateScr(string[] INFO)
    {
        Console.Clear();
        for (int i = 0; i<INFO.Length;i+=1)
        {
            if (MyPosition > INFO.Length - 1)
            {
                MyPosition = 0;
            }
            if(i == MyPosition)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine(INFO[i]);
                Console.ResetColor();
            }
            else
            {
                Console.WriteLine(INFO[i]);
            }
        }  
    }
}
