#refit

## Create API

```csharp
[Route("api/student")]
[ApiController]
public class StudentController : ControllerBase {

    public record Student(int Id, string Name);

    [HttpGet("get-students")]
    public List<Student> GetStudents() {
        return new List<Student> {
            new Student(1, "wk"),
            new Student(1, "jw"),
        };
    }

}
```

## Consume API

1. Install package

```
dotnet add src/MyApp package Refit.HttpClientFactory
dotnet add src/MyApp package Microsoft.Extensions.DependencyInject
```

2. Define API interface

```csharp
var collection = new ServiceCollection();
collection.AddRefitClient<IStudentClient>()
    .ConfigureHttpClient(c => c.BaseAddress = new Uri("http://localhost:5126"));

var service = collection.BuildServiceProvider();
var studentClient = service.GetService<IStudentClient>()!;

var students = await studentClient.GetStudents()!;
foreach (var item in students.Content) {
    Console.WriteLine($"Student (Name={item.Name}, Id={item.Id})");
}

class Student {
    public string Name { set; get; } = string.Empty;
    public int Id { set; get; }
}

interface IStudentClient {
    [Get("/api/student/get-students")]
    public Task<ApiResponse<List<Student>>> GetStudents();
}
```
