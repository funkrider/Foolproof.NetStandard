Foolproof for .Net Standard
===========================

Foolproof Validation aims to extend the Data Annotation validation provided in ASP.NET MVC.

The original repository is a clone of the MVC Foolproof Validation library from https://foolproof.codeplex.com/ with bug fixes.

This fork targets .Net Standard so it can be used in models consumed from both Core and .Net Framework applications.  Subsequently, it omits MVC validation.

Example:
```html
private class Model
{
	public string Value1 { get; set; }

	[NotEqualTo("Value1")]
	public string Value2 { get; set; }
}

[TestMethod()]
public void IsValid()
{
	var model = new Model() { Value1 = "hello", Value2 = "goodbye" };

	var ctx = new ValidationContext(model, null, null);
	var results = new List<ValidationResult>();

	bool actual = Validator.TryValidateObject(model, ctx, results, true);
	var expected = true;
	Assert.AreEqual(actual, expected);
}
```