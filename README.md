# Typescript

## Variables
+ Automatically type inference (Implicit automatically done by typescript) when initializing a variable
  + `let age = 34` - number
  + `let name = 'Josh Allen'` - string
  + `let airTicket = { id:1, name:'James Cook', no:'1234567' }` - {id:number, name:string, no: string}
  + `function getName(name){ return name; }` - function getName(name:string):string
  + `let cities = []` - any[], CAREFUL, YOU MAY WANT TO EXPLICITLY ASSIGN A TYPE TO AVOID ISSUES
+ Explicit type inference
  + `let age:number = 34`
  + `let name:string = 'Josh Allen'`
  + `let airTicket:{id:number, name:string, no: string} = { id:1, name:'James Cook', no:'1234567'}`
  + `function getName(name:string):string{ return name; }`
  + `let cities: string[] = []` or `let cities:Array<string> = []`
