

### 1. **[HttpGet]**
   - **Açıklama**: Bir HTTP `GET` isteğini işlemek için kullanılır. Genellikle veri almak amacıyla kullanılır.
   - **Kullanım**:
     ```csharp
     [HttpGet]
     public IActionResult GetProducts() { }
     ```

### 2. **[HttpPost]**
   - **Açıklama**: Bir HTTP `POST` isteğini işlemek için kullanılır. Genellikle veri oluşturma işlemleri için kullanılır.
   - **Kullanım**:
     ```csharp
     [HttpPost]
     public IActionResult CreateProduct([FromBody] Product product) { }
     ```

### 3. **[HttpPut]**
   - **Açıklama**: Bir HTTP `PUT` isteğini işlemek için kullanılır. Genellikle mevcut bir veriyi güncellemek için kullanılır.
   - **Kullanım**:
     ```csharp
     [HttpPut]
     public IActionResult UpdateProduct(int id, [FromBody] Product product) { }
     ```

### 4. **[HttpDelete]**
   - **Açıklama**: Bir HTTP `DELETE` isteğini işlemek için kullanılır. Genellikle bir kaydı silmek için kullanılır.
   - **Kullanım**:
     ```csharp
     [HttpDelete]
     public IActionResult DeleteProduct(int id) { }
     ```

### 5. **[Route]**
   - **Açıklama**: Bir denetleyici (controller) veya aksiyon metodunun URL yönlendirmesini belirler.
   - **Kullanım**:
     ```csharp
     [Route("api/products")]
     public class ProductsController : ControllerBase { }
     ```

### 6. **[FromBody]**
   - **Açıklama**: Gelen HTTP isteğindeki verileri, isteğin gövdesinden alır ve parametreye bağlar. Genellikle `POST` veya `PUT` isteklerinde kullanılır.
   - **Kullanım**:
     ```csharp
     public IActionResult CreateProduct([FromBody] Product product) { }
     ```

### 7. **[FromQuery]**
   - **Açıklama**: Verileri URL sorgu parametrelerinden alır. Genellikle `GET` isteklerinde kullanılır.
   - **Kullanım**:
     ```csharp
     public IActionResult GetProduct([FromQuery] int id) { }
     ```

### 8. **[FromRoute]**
   - **Açıklama**: URL'deki rota parametrelerinden verileri alır.
   - **Kullanım**:
     ```csharp
     public IActionResult GetProduct([FromRoute] int id) { }
     ```

### 9. **[FromHeader]**
   - **Açıklama**: HTTP isteğinin başlıklarından veri alır.
   - **Kullanım**:
     ```csharp
     public IActionResult GetProduct([FromHeader] string authToken) { }
     ```

### 10. **[Produces]**
   - **Açıklama**: Bir aksiyon metodunun hangi içerik türünde (MIME Type) çıktı üreteceğini belirtir.
   - **Kullanım**:
     ```csharp
     [Produces("application/json")]
     public IActionResult GetProducts() { }
     ```

### 11. **[Consumes]**
   - **Açıklama**: Bir aksiyon metodunun hangi içerik türünde veri alacağını belirtir.
   - **Kullanım**:
     ```csharp
     [Consumes("application/json")]
     public IActionResult CreateProduct([FromBody] Product product) { }
     ```

### 12. **[ProducesResponseType]**
   - **Açıklama**: Bir aksiyon metodunun hangi HTTP durum kodlarını döndüreceğini belirtir.
   - **Kullanım**:
     ```csharp
     [ProducesResponseType(StatusCodes.Status200OK)]
     [ProducesResponseType(StatusCodes.Status404NotFound)]
     public IActionResult GetProduct(int id) { }
     ```

### 13. **[ValidateAntiForgeryToken]**
   - **Açıklama**: CSRF saldırılarına karşı korunmak için antiforgery token doğrulaması yapar.
   - **Kullanım**:
     ```csharp
     [ValidateAntiForgeryToken]
     public IActionResult SubmitForm() { }
     ```

### 14. **[ApiController]**
   - **Açıklama**: Bu anotasyon, denetleyicinin (controller) bir API denetleyicisi olduğunu belirtir ve otomatik model doğrulama gibi özellikler sağlar.
   - **Kullanım**:
     ```csharp
     [ApiController]
     [Route("api/[controller]")]
     public class ProductsController : ControllerBase { }
     ```

---

