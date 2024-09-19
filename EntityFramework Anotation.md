Entity Framework Core'da (EF Core), ilişkiler (ilişkisel veritabanı tabloları arasındaki bağlantılar) tanımlamak için kullanılan anotasyonlar ve kavramlar oldukça önemlidir. Bu ilişkiler **one-to-many** (birden çoğa), **many-to-one** (çoktan bire) ve **many-to-many** (çoktan çoğa) gibi ilişki türlerine göre şekillenir. Ayrıca, EF Core'da bu ilişkiler modelleme ve anotasyonlarla belirlenir.

Aşağıda bu ilişkilerle birlikte en yaygın EF Core anotasyonlarını ve açıklamalarını içeren genişletilmiş bir rehber bulabilirsiniz:

---

### EF Core Anotasyonları ve İlişkiler

#### 1. **[Key]**
   - **Açıklama**: Bir sınıfın (entity) birincil anahtarını (primary key) tanımlamak için kullanılır.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [Key]
         public int ProductId { get; set; }
     }
     ```

#### 2. **[Required]**
   - **Açıklama**: Bir özellik için boş (null) değerlerin kabul edilmemesini sağlar. Bu anotasyon, veritabanındaki alanı `NOT NULL` yapar.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [Required]
         public string Name { get; set; }
     }
     ```

#### 3. **[MaxLength]**
   - **Açıklama**: Bir dize (string) özelliği için maksimum uzunluğu belirler. Veritabanındaki ilgili alanın uzunluğunu kısıtlar.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [MaxLength(100)]
         public string Name { get; set; }
     }
     ```

#### 4. **[MinLength]**
   - **Açıklama**: Bir dize (string) özelliği için minimum uzunluğu belirler.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [MinLength(5)]
         public string Description { get; set; }
     }
     ```

#### 5. **[StringLength]**
   - **Açıklama**: Hem minimum hem de maksimum uzunluğu belirler.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [StringLength(50, MinimumLength = 5)]
         public string Name { get; set; }
     }
     ```

#### 6. **[Column]**
   - **Açıklama**: Bir özelliği veritabanındaki belirli bir sütuna eşler ve sütun adı veya türü gibi ayrıntıları tanımlar.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         [Column("Product_Name", TypeName = "nvarchar(100)")]
         public string Name { get; set; }
     }
     ```

#### 7. **[Table]**
   - **Açıklama**: Bir sınıfı veritabanındaki belirli bir tabloya eşler. Tablo adını ve şemasını tanımlamak için kullanılır.
   - **Kullanım**:
     ```csharp
     [Table("Products", Schema = "dbo")]
     public class Product
     {
         public int ProductId { get; set; }
         public string Name { get; set; }
     }
     ```

---

### İlişki Anotasyonları (One-to-Many, Many-to-One, Many-to-Many)

#### 8. **[ForeignKey]**
   - **Açıklama**: Bir özelliği yabancı anahtar (foreign key) olarak işaretler. Genellikle ilişkisel (one-to-many, many-to-one) tablolar arasında bağlantı kurarken kullanılır.
   - **Kullanım**:
     ```csharp
     public class Order
     {
         public int OrderId { get; set; }

         [ForeignKey("Customer")]
         public int CustomerId { get; set; }
         public Customer Customer { get; set; }
     }
     ```

#### 9. **[InverseProperty]**
   - **Açıklama**: İki yönlü ilişkilerde (one-to-many veya many-to-many) karşılıklı ilişkileri tanımlar. Bu anotasyon, ilişkili sınıflar arasında bağlantıyı belirlemeye yardımcı olur.
   - **Kullanım**:
     ```csharp
     public class Customer
     {
         public int CustomerId { get; set; }

         [InverseProperty("Customer")]
         public ICollection<Order> Orders { get; set; }
     }

     public class Order
     {
         public int OrderId { get; set; }

         [ForeignKey("Customer")]
         public int CustomerId { get; set; }
         public Customer Customer { get; set; }
     }
     ```

---



#### 10. **[NotMapped]**
   - **Açıklama**: Bir özelliğin veritabanına haritalanmasını engeller. Bu özellik yalnızca uygulama içinde kullanılır, veritabanında karşılık gelen bir sütun oluşturulmaz.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         public int ProductId { get; set; }
         public string Name { get; set; }

         [NotMapped]
         public string TemporaryProperty { get; set; }
     }
     ```

#### 11. **[ConcurrencyCheck]**
   - **Açıklama**: Bu anotasyon, bir alanın eşzamanlılık (concurrency) denetimi için kullanılmasını sağlar.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         public int ProductId { get; set; }

         [ConcurrencyCheck]
         public string Name { get; set; }
     }
     ```

#### 12. **[Timestamp]**
   - **Açıklama**: Eşzamanlılık kontrolü yapmak için zaman damgası (timestamp) sütunu olarak kullanılır.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         public int ProductId { get; set; }

         [Timestamp]
         public byte[] RowVersion { get; set; }
     }
     ```

#### 13. **[Index]**
   - **Açıklama**: Bel

irtilen sütun(lar) üzerinde bir indeks oluşturur.
   - **Kullanım**:
     ```csharp
     [Index(nameof(Name), IsUnique = true)]
     public class Product
     {
         public int ProductId { get; set; }
         public string Name { get; set; }
     }
     ```

#### 14. **[Precision]**
   - **Açıklama**: Sayısal (decimal) verilerde hassasiyet (precision) ve ölçek (scale) tanımlamak için kullanılır.
   - **Kullanım**:
     ```csharp
     public class Product
     {
         public int ProductId { get; set; }

         [Precision(18, 2)]
         public decimal Price { get; set; }
     }
     ```

---

