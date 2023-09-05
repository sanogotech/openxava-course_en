# openxava-course_en
Source code for OpenXava course in English

## Docs

- https://www.openxava.org/OpenXavaDoc/docs/getting-started_en.html
- https://www.openxava.org/OpenXavaDoc/docs/basic-domain-model1_en.html
- Annotation full docs: https://www.openxava.org/OpenXavaDoc/docs/model_en.html#Model-Properties-Stereotype
- View : https://www.openxava.org/OpenXavaDoc/docs/view_en.html


##  Architecture

* https://www.openxava.org/OpenXavaDoc/docs/philosophy_en.html

   the Invoice class. This class contains code dealing with persistence, data structures, business logic, user interface, validation, etc.
This is accomplished using the Java metadata facility, so-called annotations. These are the annotations used in this example:

| Facet          | Metadata                                | Implemented by   |
| ---------------| ---------------------------------------| ----------------- |
| Database       | @Entity, @Table, @Id, @Column, @ManyToOne | JPA             |
| User interface | @View, @DescriptionsList                | OpenXava         |
| Validation     | @Max, @Required                         | Bean Validation, OpenXava |
| Business logic | @DefaultValueCalculator                | OpenXava         |


Thanks to metadata you can do most of the work in a declarative way and the dirty work is done for you by JPA (the Java standard for persistence), Bean Validation (the Java standard for validation) and OpenXava.
Moreover, the code you write is plain Java, like properties (year and seller, 1) for defining the data structure, and methods (applyDiscounts(), 2) for programmatic business logic.
All you need to write about invoice is Invoice.java. It is a Business Component. The magic of OpenXava is that it transforms this Business Component into a ready to use application.

```java
/**
 * A Java class for defining a business component.
 */
 
@Entity  // Database
@Table(name="GSTFCT")  // Database
@View(members=  // User interface
    "year, number, date, paid;" +
    "customer, seller;" +
    "details;" +
    "amounts [ amountsSum, vatPercentage, vat ]"
)
public class Invoice {
 
    @Id  // Database
    @Column(length=4)  // Database
    @Max(9999)  // Validation
    @Required  // Validation
    @DefaultValueCalculator(  // Declarative business logic
        CurrentYearCalculator.class
    )
    private int year;  // Data structure (1)
 
    @ManyToOne(fetch=FetchType.LAZY)  // Database
    @DescriptionsList     // User interface
    private Seller seller;  // Data structure
 
    public void applyDiscounts() {  // Programmatic business logic (2)
        ...
    }
 
    ...
}

```
## Business Component

The basic unit to create an OpenXava application is the business component. A business component is defined using a Java class called Entity. This class is a regular EJB3 entity, or in other words, a POJO class with annotations that follows the Java Persistence API (JPA) standard.
JPA is the Java standard for persistence, that is, for objects that store its state in a database. If you know how to develop using POJOs with JPA, you already know how to develop OpenXava applications.
Using a simple Java class you can define a Business Component with:

- Model: Data structure, validations, calculations, etc.
- View: How the model can be shown to the user.
- Tabular data: How the data of the component is displayed in list mode (in tabular format).
- Object/relational mapping: How to store and retrieve the object state from database.
  
This chapter explains how to define the model part, that is, all about structure, validations, calculations, etc.

##  Model

![ Sample Model](https://github.com/sanogotech/openxava-course_en/blob/lesson-26/images/SampleDomainModel.png)

## Properties

Properties
A property represents the state of an object that can be read and in some cases updated. The object does not have the obligation to store physically the property data, it only has to return it when required.
The syntax to define a property is:

```java
@Stereotype                                                                //  1
@Column(length=) @Column(precision=) @Max @Length(max=) @Digits(integer=)  //  2
@Digits(integer=) @Digits(fraction=)                                       //  3
@Required @Min @Range(min=) @Length(min=)                                  //  4
@Id                                                                        //  5
@Hidden                                                                    //  6
@SearchKey                                                                 //  7
@Version                                                                   //  8
@Formula                                                                   //  9  New in v3.1.4
@Calculation                                                               // 10  New in v5.7
@DefaultValueCalculator                                                    // 11
@PropertyValidator                                                         // 12
private type propertyName;                                                 // 13
public type getPropertyName() { ... }                                      // 13
public void setPropertyName(type newValue) { ... }                         // 13
 
```

## View

- https://www.openxava.org/OpenXavaDoc/docs/view_en.html
