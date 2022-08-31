# CleanCodeQoidalari

**1. O'zgaruvchilarga ma'noli nom berish**
```cs
// Yaxshi:
string accountNumber = "";
int studentId = 1012;
double weatherSpeed = 0;

// Yomon:
int abc123;
string myVar = "";
object customer22;
bool data;
```


**2. PascalCase va camelCase uslublaridan to'g'ri foydalanish**

```cs
// a.Klass miqyozidagi xossalarni ko'rinish doirasi odatda public bo'ladi.

// Shuning uchun ularni nomlashda PascalCase ishlataman.

public DateTime BusinessDate { get; set; }
public double TransferAmount { get; set; }

// b.Klass miqyozidagi ko'rinish doirasi private bo'lgan,

// ichki o'zgaruvchilarni nomlashda ularni ostki chiziqcahdan boshlab _,

// camelCase dan foydalanaman.

private int _foldersCount;
private string _targetFileName;

// c.Metodlarni nomlashda PascalCasing ishlataman.
public void GenerateToken()
{

}

// d.Metodning parametrlarini nomlashda camelCase dan foydalanaman.

private bool Connect(string serverName, int port)
{
    //...
    return true;
}
```


**3. Kod qatorlarini formatlanishi. Ctrl+K+D**


**4. Sharxlarni faqat kerakli joyda ishlatish.**
- Sharxlar kodni nima ish bajarishini ta'riflaydi, qanday bajarishini emas.

```cs
/// <summary>
/// This method initializes all the variables with their default values
/// </summary>
public void Initialize()
{

}
```


**5. Sehrli sonlardan foydalanmaslik (no to magic numbers!)** 
- `const` yoki `config`!

```cs
// Yomon:
void ValidateAge(int age)
{
    if (age < 18)
    {
        // logic here
    }
}

// Yaxshi:
const int MINIMUM_AGE = 18;
void ValidateUsersAge(int age)
{
    if (age < MINIMUM_AGE)
    {
        // logic here
    }
}
```


**6. Ishlatilmaydigan kodlarni o'chirib tashlash.**


**7. bir qatorli metodlarni lambda expression ko'rinishida yozish**
```cs
public string Greet(string name) => $"Assalomu alaykum, {name}";
```


**8. Metodning hajmiga e'tibor berish.**


**9. Matnlarni birlashtirishda interpolation yoki StringBuilder ishlatish**
```cs
static string firstName = "Farkhod";
static string lastName = "Dadajanov";

// Yomon:
static string fullNameBad = "Mr. " + firstName + " " + lastName + ".";

// Yaxshi (C#6 dan boshlab):
static string fullNameGood = $"Mr. {firstName} {lastName}.";


// Yomon:
string GetLongNumberBad()
{
    string result = "";
    for (int i = 0; i < 100000; i++)
    {
        result += i;
    }
    return result;
}

// Yaxshi:
string GetLongNumberBetter()
{
    var builder = new StringBuilder();
    for (int i = 0; i < 100000; i++)
    {
        builder.Append(i);
    }
    return builder.ToString();
}
```


**10. Qisqa if-tekshiruvlari uchun Ternary operatoridan foydalanish**

```cs
// So-so:
const int MINIMUM_SCORE = 65;
public string GetResultSoSo(int score)
{
    if (score >= MINIMUM_SCORE)
    {
        return "Success";
    }
    else
    {
        return "Fail";
    }
}

// Better:
public string GetResultOk(int score)
{
    return score > MINIMUM_SCORE ? "Success" : "Fail";
}

public string GetResultGood(int score) =>
        score > MINIMUM_SCORE ? "Success" : "Fail";
```


**11. Metod parametrlari sonini 4 tadan oshirmaslik**

```cs
// Yomon:
public void CreateStudent(string firstName, string lastName, int age, bool isMale)
{
    // logic
}


// Yaxshi:
public void CreateStudent(Student student)
{
    // logic
}
```


**region yordamida mantiqan bir ishni bajaruvchi kodlarni birlashtirish** 
- `Ctrl+M+O` - yopish, `Ctrl+M+L` - ochish 

```cs
#region Initialization
// some codes here
#endregion

#region Public methods
// some codes here
#endregion

#region Events
// events
#endregion
```


**13. Ishlailmagan using'larni o'chirib tashlash**


**14. Warning'larga e'tibor berish**
- Code Analyzer'ni yoqish
```cs
<AnalysisLevel>latest-Recommended</AnalysisLevel>

```


**15. Unit Test'lar dan foydalanish**


**16. SOLID, DRY va KISS tamoyillariga amal qilish**


**17. Design Pattern'lardan kerakli joylarda foydalanish** 
- `Singleton`, `Factory method`, `Adapter`, `Facade`, `Command`, `Mediator`, `Observer`
