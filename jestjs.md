# JEST and react testing library

Testing by developer

- unit testing testing individual units or components
- integration testing Testing between two units or componets
- E2E testing test start to end complete project

@testing-library/jest-dom
@testing-library/react
@testing-library/user-event

app.test.js

```js
import {render,screen} from "@testing-library/react";
import App from "./App";

test('render learn react link,()=>{
    render(<App/>);
    const linkElement=screen.getByText(/learn react/i);
    expect(linkElement).toBeInTheDocument()
})
```

--> package.json

"test":"react-script test"

or npm i jest
npm run jest

sum.js
export default function sum(a,b){
return a+b;
}

.test.js

defination , callbackfunction, excecute after x seconds

.test.js

```js
test("defination", () => {
  expect(sum(10, 10)).toBe(20);
});
```

--> if want to use JSX

> > npm install --save-dev @babel/preset-env @babel/preset-react babel-jest

Then create a .babelrc file in your project root:
{
"presets": ["@babel/preset-env", "@babel/preset-react"]
}

--> get element by text
.getByText("")
.tpBeInTheDOcument()


--> get element which have title 
.getByTitle("")

### test input tag
<input type="text" placeholder=""/>
.getByRole("textbox")
 
screen.getByPlaceholderText(""); // Matches input by placeholder

screen.getByLabelText("Your Label"); // If there's an associated <label>

--> this check name attribute
expect(checkInput).toHaveAttribute("name","username") 
expect(checkInput).toHaveAttribute("id","user_name")

### run specific file and run specific file test

npm run test filename (App)

### Test Grouping with describe
```js
describe("URI test case group",()=>{
  test("render learn react link",()=>{
    render(<App/>);
    const linkElement=screen.getByText(/learn react/i);
    expect(linkElement).toBeInTheDocument()
   })
    test("render learn react link 2",()=>{
    render(<App/>);
    const linkElement=screen.getByText(/learn react/i);
    expect(linkElement).toBeInTheDocument()
   })
})

describe.only --> this only run describe
describe.skip --> this skip describe


we can have nested describe inside a describe

```

### on change event with input box

render(<App>)
let input =screen.getByRole("textbox");
fireEvent.change(input,{target:{value:"a"}});
expect(input.value).toBe("a")

### on change event with button
render(<App/>)
const btn=screen,getByRole("button)
fireEvent.click(btn);
expect(screen.getByText("updated data)).toBeInTheDocument()

file_naming
test.test.js --> file extension
.spec.js --> file extension
spec.jsx --> file extension

__tests__  folder --> all file inside this consider as test file
can extension is not madetory

###  Before and After Hooks
--> beforeAll 
use to clear somethings or setup env 
it before any test run
beforeAll(()=>{
  console.log("")
})

--> beforeEach

beforeEach(()=>{
  console.log("")
})

run before each test


--> AfterAll 
same as before

--> AfterEach

### Snapshot testing
const container=render(<App/>)
.toMatchSnapshot();
expect(container).toMatchSnapshot();

this create a  snap and when run again it will check whether the code is matching  previous snap

### function component method testing

.toMatch("hi")

###  RTL query ( to find a element )
##### -->  GetByRole

.getByTestId("")

* this check default value of input tag
expect(inputField).toHaveValue("hello")

* this check whether a tag is diabled or not
toBeDiabled()

###### ---> multiple element with role custom role
.getByRole("button",{name:""})
role and attributes 

for an input tag its label name is its name

for non sementic element
<div role="custom-role"></div>


##### -->  GetAllByRole
const btns=screen.getAllByRole("button")
for(let i =0;i<btns.length;i++>){
 btn[i]
}


##### -->  getByLabelText()
##### -->  getAllByLabelText()
##### -->  getByPlaceholderText()
##### -->  getAllByPlaceholderText()
##### -->  getByText()
##### -->  getAllByText()
##### -->  getByTestId()  data-testid=""
##### -->  getAllByTestId()

### Overrriding data-testid
import {configure} from "@testing-libbrary/react"
configure(
  {
    testIdAttribute:"element-id"
  }
)

##### -->  getByDisplayValue()

##### -->  getAllByDisplayValue()
this is for default value check

##### -->  getByTitle()

##### -->  getAllByTitle()


these work with title atribute

##### -->  getAllByAltText()
##### -->  getByAltText()

image alt text

### Priority order for RTL queries

### Assertion Method
* .toBeInTheDocument()
* .toHaveValue()  -->  check default value
* .toHaveValue("value")  -->  check default value
* .toBeEnable() or .toBeDisabled --> check disabled 
* .toHaveAttribute("alt") --> check attribute
* .toHaveClass("class")
* .not.any Assertion

### Test match with string and regex


.getByText("Hello World",{exact:false})
.getByText(/Hello World/)
.getByText(/Hello World/i)
.getByText(/Hello W?orld/i) w is not sure

### Text Match with function
.getByText((contenet,element)=>content.startsWith("Hello"))

.getByText((contenet,element)=>content.endsWith("Hello"))

.getByText((contenet,element)=>{
  return content.startsWith("Hello")
})

content is text inside tag

### QueryBy and queryAllBy

* screen.getByText("asd") --> this get based upon ui
* screen.getByQuery("Login") --> this check in complete file

### FindBy and FindByAll
await .findByText()
works only if text is in document with in 1s

await .findByText("",{},{timeout:5000})

how it works with 5s it can have till 5s

### Js Query or custom query
document.querySelector("#testId")

### Querying Within Elements
find element within an elements

used when we what to check a parent must have specific tag
let el =screen.getByText("Hello")
let subEl=within(el).getByText("hi")

### CLick Event WIth User Event
on change in input box

```js

import userEvent from "@testing-libraray/user-event";
test("On CHnage event testing",async ()=>{
  userEvent.setup()
render(<App/>);
const el=screen.getByRole("textBox")
await userEvent.type(el,"anil") // this type in the input element , we need to use async when we use userEvent
expect(screen.getByText("anil")).toBeInTheDocument();
})
```

### Act function

```js

import userEvent from "@testing-libraray/user-event";
test("On CHnage event testing",async ()=>{
  userEvent.setup()
render(<App/>);
const el=screen.getByRole("textBox")
await act(async ()=>{ await userEvent.type(el,"anil")}) // this type in the input element , we need to use async when we use userEvent
expect(screen.getByText("anil")).toBeInTheDocument();
})
```

### test component props
<User name="anil"/>

```js
test("Props testing",()=>{
  render(<User name="sachin">)
  const user=screen.getByText("sachin");
  expect(user).toBeInTheDocument()
})

```

### Functional Props testing and mocking

test("functional props testing",()=>{
  const testFunction=jest.fn();
  userEvent.setup();
  render(<App testFunction={testFunction}/>);
  const btn=screen.getByROle("button")
  await userEvent.click(btn);
  expect(testFunction).toBeCalled()

})

### MSW and Http Request testing

MSW --> mock service worker
we mock api to save server and cost and is complex

mockServices/server.js and handler.js
handler.js
import {rest} from "msw";

export const handler=[
  rest.get("endpoint",)
]






