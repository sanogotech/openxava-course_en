# openxava-course_en
Source code for OpenXava course in English

## Docs

- https://www.openxava.org/OpenXavaDoc/docs/getting-started_en.html
- https://www.openxava.org/OpenXavaDoc/docs/basic-domain-model1_en.html
- Annotation full docs: https://www.openxava.org/OpenXavaDoc/docs/model_en.html#Model-Properties-Stereotype
- View : https://www.openxava.org/OpenXavaDoc/docs/view_en.html

##  Model

![ Sample Model](https://github.com/sanogotech/openxava-course_en/blob/lesson-26/images/SampleDomainModel.png)

## Properties

Properties
A property represents the state of an object that can be read and in some cases updated. The object does not have the obligation to store physically the property data, it only has to return it when required.
The syntax to define a property is:

```
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
