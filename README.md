# Typescript
Typescript uses structural type checking instead of nominal type checking. Typescript uses static typying instead of dynamic typing like javascript.

+ Setting VS Code: https://code.visualstudio.com/docs/typescript/typescript-compiling
+ https://www.typescript-training.com/course/fundamentals-v4

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
+ `const name = "Josh"` this is the same as the point above
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

## Index Signatures ({[prop:string]:any})
```
const obj: {[prop:string]:string} = {}; // this obj can have a property assigned to it that is of type string and its value is also of type string

obj.color = "green" //✅ this works because the property is of type string and its value is of type script

obj.color = 64 //❌ this would not work because the property value type is a number but we typed the value as a string. For this to work you will need to change the property value type to type `any`

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
    type CarType = [string, number, boolean]

    let car: CarType = ['mustang', 8, true];

    console.log(car[2])
```
  + NOTES: The length of the tuple when using `car.length` may just be giving you the  count of the types in the type annotation not the count of the elements in the array when using methods like `pop`, `push` from the javascript array object!
  + You can use `readonly` to prevent the usage of those methods (from javascript array object)!
  + `readonly` makes the data inmutable so you would not be able to change the data individually
```
    let car: readonly [string, number, boolean] = ['mustang', 8, true];

    //or

    type CarType = readonly [string, number, boolean]

    let car: CarType = ['mustang', 8, true];

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

    //or
    type onOff = 0 | 1 | boolean;

    let isAvailable = 1; //isAvailable can only take the following values: 0, 1, true, false

    console.log(isAvailable);
 ```
+ Intersection - AND &
```
        XXXXXXXXX     XXXXXXXXX       
    XXX         XXXXX         XXX    
  XX            XX▒XX            XX  
 X             X▒▒▒▒▒X             X 
X             X▒▒▒▒▒▒▒X             X
X             X▒▒▒▒▒▒▒X             X
X             X▒▒▒▒▒▒▒X             X
 X             X▒▒▒▒▒X             X 
  XX            XX▒XX            XX  
    XXX         XXXXX         XXX    
       XXXXXXXXX     XXXXXXXXX       
```  
```
  type Evens = 2 | 4 | 6 | 8;
  type ToFive = 1 | 2 | 3 | 4 | 5;

  let nums: Evens & ToFive = 2

  console.log(nums);
```

## Type Aliases And Interfaces
Provides a name to the shape of the custom type

+ Type Aliases
```
type Name = string | null;

let firstName:Name = null;
let lastName:Name = "Allen";

console.log(firstName);
console.log(lastName);

//Sample
type MyDate = Date & {getMessage(): string};
const d: MyDate = Object.assign(new Date(), {getMessage: () => "New Year!"})

console.log(d.getMessage())

//Sample
type Player = {
    name: string
    number: number
    position: string
}

let quarterback: Player = {
    name: "Josh Allen",
    number: 17,
    position: "Quarterback",
}

let runningBack: Player = {
    name: "James Cook",
    number: 4,
    position: "Running back",
}

console.log(quarterback)
console.log(runningBack)

function getPlayerName(player: Player): string {
    return player.name;
}

console.log(getPlayerName(quarterback))
console.log(getPlayerName(runningBack))
```
+ Interfaces
  +  Extends
```
//Sample 1
interface Player {
    name: string
    number: number
}

function getPlayerName(player: Player): string {
    return player.name;
}

console.log(getPlayerName({name: 'Josh Allen', number: 17}))

//Sample 2
interface Person {
    name: string
}

interface Player extends Person {
    number: number
    position: string
}

function getPlayerName2(player: Player): string {
    return player.name;
}

console.log(getPlayerName2({name: 'Josh Allen', number: 17, position: 'quarterback'}))
```
  +  Implements 
```
interface Player {
    name: string;
    number:number
    position:string
    getName():string
}

class FootballPlayer implements Player {
    constructor(public name: string, public number:number, public position:string) {
        this.name = name;
        this.number = number;
        this.position = position;
    }

    getName(): string {
        return this.name;
    }

    getPosition():string{
        return this.position;
    }
}

let p = new FootballPlayer("Josh Allen", 17, 'quarterback');

console.log(p.getName());
console.log(p.getPosition());
```
+ Interfaces are OPEN (NOT TYPE ALIAS) - meaning you can modify them (add) new properties or methods after they have been declared
```
interface Player {
    name: string;
    number: number
    position: string

    getName(): string
}

class FootballPlayer implements Player {
    name = "";
    number = 0;
    position = "";
    height = 0;

    constructor(name: string, number: number, position: string, height: number) {
        this.name = name;
        this.number = number;
        this.position = position;
        this.height = height
    }

    getName(): string {
        return this.name;
    }

    getPosition(): string {
        return this.position;
    }
}

interface Player {
    height: number
}

let p = new FootballPlayer("Josh Allen", 17, 'quarterback', 6.5);

console.log(p.getName());
console.log(p.getPosition());
```
+ Modifying the global object
```
const message = "This message export is here for the declare global to work";

declare global {
    interface Window {
        myProperty: string
    }
}

window.myProperty

export default message
```

## Recursive Types
```
type MyNumbers = number | MyNumbers[] //here the myNumbers is recursive

let nums:MyNumbers = [1,2,[3,[4],5],6,7]

console.log(nums)
```

## Type Queries
+ keyof
```
type DateProperties = keyof Date

type DateStringProperties = DateProperties & string
type DateSymbolProperties = DateProperties & symbol
```
+ typeof - here is extracting the shape of response and creating a type `myResponse`. This is different from using typeof in a conditional to see if variable if of the required type.
```
const response = {
    status: 200,
}

type MyResponse = typeof response

//MyResponse = { status: number }
```
+ Index access types
```
interface Year {
    dayName: string;
    dayNumber: number;
    monthName: string;
    monthNumber: number;
    time:{
      hours:number;
      minutes:number;
    }
}

let x: Year["dayNumber"] = 7
let y: Year["dayName" | "monthNumber"] = "Friday"
let z: Year["dayName" | "monthNumber"] = 3
let a: Year["time"]["hours"] = 23

console.log(x, y, z, a)
```

## Callables (Function Declaration)
```
//Interface
interface AddFunI {
    (a: number, b: number): number;
}

const add1:AddFunI = (a: number, b: number) => a + b;

console.log(add1(2,2))

//Type Alias
type AddFunT = (a: number, b: number) => number;

const add2:AddFunT = (a: number, b: number) => a + b;

console.log(add2(5,5))
```

## Void
This means to ignore the retrun type no matter what it is
```
function invoke(fn: () => undefined) {
    setTimeout(fn, 1);
}

function invoke2(fn: () => void) {
    setTimeout(fn, 1);
}

const vals: number[] = [];

invoke(()=>vals.push(4)) //here since push returns a number and the invoke callback has a return type of undefined, we run into an issue.
invoke2(()=>vals.push(4)) //here since the invoke2 callback type is void, it really does not matter what push returns.  Void ignores the return value.
```

## Classes
```
type Gender = "m" | "f" | "male" | "female" | "na";

class Human {
    static type: string = "human"; //static means to be used without instantiating the class
    protected version: string = "v1.0" //protected means it can only be used/seen by the subclasses but not a new instance of Human
    private _name: string; //private means to only be used internally in the class
    private _age: number; //private means to only be used internally in the class
    private _gender: Gender

    constructor(name: string, age: number, gender: Gender) {
        this._name = name;
        this._age = age;
        this._gender = gender;
    }

    get name(): string {
        return this._name;
    }

    set name(value: string) {
        this._name = value;
    }

    get age(): string {
        return this._age.toString();
    }

    get gender(): string {
        if (this._gender === "male")
            return "male";
        else if (this._gender === "female")
            return "female";

        return this._gender.toString();
    }

    set gender(value: Gender) {
        this._gender = value;
    }

}

let h = new Human("Jenny", 21, "f")

h.name = "Jane"
console.log(h.name);
console.log(h.age)
console.log(h.gender)
console.log(Human.type)
```
+ Param Properties
```
type Gender = "m" | "f" | "male" | "female" | "na";

class Human {
    static readonly type: string = "human"; //static means to be used without instantiating the class, readonly means it can not be changed but only read
    protected version: string = "v1.0" //protected means it can only be used/seen by the subclasses but not a new instance of Human

    constructor(private _name: string,
                private _age: number,
                private _gender: Gender) {
    }

    get name(): string {
        return this._name;
    }

    set name(value: string) {
        this._name = value;
    }

    get age(): string {
        return this._age.toString();
    }

    get gender(): string {
        if (this._gender === "male")
            return "male";
        else if (this._gender === "female")
            return "female";

        return this._gender.toString();
    }

    set gender(value: Gender) {
        this._gender = value;
    }

}

let h = new Human("Jenny", 21, "f")

h.name = "Jane"
console.log(h.name);
console.log(h.age)
console.log(h.gender)
console.log(Human.type)
```
