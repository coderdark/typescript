# Typescript
Typescript uses structural type checking instead of nominal type checking. Typescript uses static typying instead of dynamic typing like javascript.

## Primitives Types - use the lowercase names!
+ `number`
+ `string`
+ `boolean`
+ `bigint` - new version of typescript
+ `symbol` - new version of typescript

## Special Types
+ `any` - disables checking and you can assign any type to the variable that has this defined type
+ `unknown` - safer alternative to type `any`
+ `never` - throws error whenever is defined
+ `null` - native javascript type primitive use in typescript
+ `undefined` - native javascript type primitive use in typescript
  
## Variables
+ Automatically type inference (Implicit automatically done by typescript) when initializing a variable
  + `let age = 34` - number
  + `let name = 'Josh Allen'` - string
  + `let airTicket = { id:1, name:'James Cook', no:'1234567' }` - {id:number, name:string, no: string}
  + `function getName(name){ return name; }` - function getName(name:string):string
  + `let states = []` - any[], CAREFUL, YOU MAY WANT TO EXPLICITLY ASSIGN A TYPE TO AVOID ISSUES OR INCLUDE VALUES TO THE ARRAY SO TYPESCRIPT CAN TYPE INFER THE TYPE OF ARRAY ie: `let states = ['Michigan', 'Colorado']` this tells typescript this is a string array, string[].
+ Explicit type inference (type annotations, ei: number, string, boolean)
  + `let age:number = 34`
  + `let name:string = 'Josh Allen'`
  + `let airTicket:{id:number, name:string, no: string} = { id:1, name:'James Cook', no:'1234567'}`
  + `function getName(name:string):string{ return name; }`
  + `let cities: string[] = []` - prefer way of type annotation for arrays
  + `let cities:Array<string> = []` - here using generics T<U>, CAREFUL IF USING REACT THIS TYPE FORMAT CAN CREATE ISSUES!  STICK TO THE TYPE ANNOTAION ABOVE.

## Type Assertions
+ `let name = "Josh" as "Josh"` - here the variable 'name' can only accept the value "Josh" and nothing else otherwise it throws an error
+ `let canvas = document.getElementById("gameCanvas") as HTMLCanvasElement` - here typescript does automatic type inference to a `HTMLElement` if you want to be more explicit you can use a type assertion to make sure your canvas is of type  `HTMLCanvasElement` instead of the default type `HTMLElement`

## Optionals
```
  const car: {
    id:string
    model:string
    cylinders:number
    sport:boolean
    electric?:boolean //the ? marks the property as optional
  }
```

## Index Signatures
```
const obj: {[prop:string]:string} = {}; // this obj can have a property assigned to it that is of type string and its value is also of type string

obj.color = "green" //✅ this works because the property is of type string and its value is of type script

obj.color = 64 //❌ this would not work because the value type is a number but we typed the value as a string

const phone: { [prop: string]: { number: string } } = {};

phone.home = {number: "479.678.5555"};
phone["cell"] = {number: "479.143.5555"}; //best practice to use the dot notation format as the above

console.log(phone.home);
```

## Arrays
+ Assignment
  + Simple: `let grades: number[] = []`
  + Complex:
```
      const cars:{model:string, cylinders:number, sport:boolean}[] = [
        {
            model:'mustang',
            cylinders:8,
            sport:true,
        },
        {
            model:'silverado',
            cylinders:8,
            sport:false,
        }
    ]

    console.log(cars)
```
+ Two dimentional array `let grades: number[][] = [[100,100,90,80], [80,80,50,100]]`
  
## Tuples
+ Assignment
  + Simple: `let car: [string, number, boolean] = ['mustang', 8, true];` - creates an array of specific member count, in this case this array can only have 3 members.
  + Complex: 
```
    type carType = [string, number, boolean]

    let car: carType = ['mustang', 8, true];

    console.log(car[2])
```
  + NOTES: The length of the tuple when using `car.length` may just be giving you the  count of the types in the type annotation not the count of the elements in the array when using methods like `pop`, `push` from the javascript array object!
  + You can use `readonly` to prevent the usage of those methods (from javascript array object)!
  + `readonly` makes the data inmutable so you would not be able to change the data individually
```
    let car: readonly [string, number, boolean] = ['mustang', 8, true];

    //or

    type carType = readonly [string, number, boolean]

    let car: carType = ['mustang', 8, true];

    console.log(car[2])
```
## Unions and Intersection Types            
+ Union - OR |
```
       XXXXXXXXX     XXXXXXXXX       
    XXX▒▒▒▒▒▒▒▒▒XXXXX▒▒▒▒▒▒▒▒▒XXX    
  XX▒▒▒▒▒▒▒▒▒▒▒▒XX▒XX▒▒▒▒▒▒▒▒▒▒▒▒XX  
 X▒▒▒▒▒▒▒▒▒▒▒▒▒X▒▒▒▒▒X▒▒▒▒▒▒▒▒▒▒▒▒▒X 
X▒▒▒▒▒▒▒▒▒▒▒▒▒X▒▒▒▒▒▒▒X▒▒▒▒▒▒▒▒▒▒▒▒▒X
X▒▒▒▒▒▒▒▒▒▒▒▒▒X▒▒▒▒▒▒▒X▒▒▒▒▒▒▒▒▒▒▒▒▒X
X▒▒▒▒▒▒▒▒▒▒▒▒▒X▒▒▒▒▒▒▒X▒▒▒▒▒▒▒▒▒▒▒▒▒X
 X▒▒▒▒▒▒▒▒▒▒▒▒▒X▒▒▒▒▒X▒▒▒▒▒▒▒▒▒▒▒▒▒X 
  XX▒▒▒▒▒▒▒▒▒▒▒▒XX▒XX▒▒▒▒▒▒▒▒▒▒▒▒XX  
    XXX▒▒▒▒▒▒▒▒▒XXXXX▒▒▒▒▒▒▒▒▒XXX    
       XXXXXXXXX     XXXXXXXXX
```
 ```
    let isAvailable: 0 | 1 | boolean = 1; //isAvailable can only take the following values: 0, 1, true, false

    console.log(isAvailable);
 ```
+ Intersection - AND &
```
       XXXXXXXXX     XXXXXXXXX       
    XXX         XXXXX         XXX    
  XX            XXXXX            XX  
 X             XXXXXXX             X 
X             XXXXXXXXX             X
X             XXXXXXXXX             X
X             XXXXXXXXX             X
 X             XXXXXXX             X 
  XX            XXXXX            XX  
    XXX         XXXXX         XXX    
       XXXXXXXXX     XXXXXXXXX
```  
```
    let isAvailable: 0 | 1 | boolean = 1; //isAvailable can only take the following values: 0, 1, true, false

    console.log(isAvailable);
```
