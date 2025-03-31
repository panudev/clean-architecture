# 🧼 Clean Architecture - ASP.NET Core Example

An example project structure based on Clean Architecture using ASP.NET Core (Web API).  
Ideal as a scaffold for building medium to large-scale applications, with a clear separation of concerns between each layer.

---

## 🏗️ Project Structure

```plaintext
/CleanArchitecture
├── CleanArchitecture.API/                  <-- Presentation Layer (Controllers, Middleware, DTOs)
├── CleanArchitecture.Application/          <-- Application Layer (Use Cases, Services, Interfaces)
├── CleanArchitecture.Domain/               <-- Domain Layer (Entities, Value Objects, Interfaces)
├── CleanArchitecture.Infrastructure/       <-- Infrastructure Layer (EF, Redis, File System, etc.)
```

---

## 🧠 Clean Architecture Overview

- **Domain**: Core business rules, independent from any framework or technology.
- **Application**: Coordinates use cases and business logic orchestration.
- **Infrastructure**: Implements repositories and external services.
- **API**: The entry point for external communication (e.g., Web API).

**Dependency Rule:**  
Dependencies should only flow **inward** (Outer → Inner).

```
API --> Application --> Domain
Infrastructure --> Application / Domain
```

---

## 🚀 How to Run

### ✅ Prerequisites

- [.NET 9 SDK](https://dotnet.microsoft.com/en-us/download)
- IDE of your choice: Visual Studio, VS Code, or Rider

---

### 🛠️ Restore & Build

```bash
dotnet restore
dotnet build
```

---

### ▶️ Run the API

```bash
dotnet run --project CleanArchitecture.API
```

---

### 🔁 Example API Call

```http
GET /api/user/{id}
```

---

## 🔌 Dependency Injection Setup

In `Program.cs`:

```csharp
builder.Services.AddScoped<IUserRepository, InMemoryUserRepository>();
builder.Services.AddScoped<UserService>();
```

---

## 🧪 Testing

Each layer is designed to be testable in isolation without tight coupling to ASP.NET or EF Core.  
For example:

```csharp
[Test]
public async Task Should_Return_User_If_Exists() {
    var repo = new InMemoryUserRepository();
    var service = new UserService(repo);

    var result = await service.GetUserAsync(userId);

    Assert.NotNull(result);
}
```

---

## 🧱 Why Clean Architecture?

- Easy to test (Testable)
- Technology-agnostic and maintainable
- Encourages clean, decoupled code
- Scales well with growing application complexity

---

## 📦 Ready for Extensions

- ✅ Add EF Core / Dapper
- ✅ Integrate Redis / Message Queue
- ✅ Dockerize with CI/CD pipelines
- ✅ Add Logging, Validation, Authentication, Middleware