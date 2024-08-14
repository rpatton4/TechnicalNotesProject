# Entity Framework Core

## Defining a table/entity
- No special indicator at the class level
- Public properties become table columns
- The primary key is identified one of 3 ways: naming it `Id`,
  naming it `<class name>Id`, or using the attribute `[Key]` for the property

## Null values
- For properties, if you want to require a property to be non-null, you can
  either use the attribute `[Required]` with a nullable type (for ex. `string?`)
  which would allow null in the model but not the DB, or you can just have
  a property which is not nullable and initialize it using the `= null!` to 
  tell the compiler I know what I'm doing. For ex.,`Public string FirstName 
  { get; set;} = null!;` which works because EF will ensure the property is not
  null when it matters.