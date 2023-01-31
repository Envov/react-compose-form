**this repo plan to realize below code fragment**

```tsx
import {Input} from "some-components"
import {field,placeholder,key,component,props,style,value,className,onInput} from "react-compose-form"
import {reaction,when,or,and,eq} from "react-compose-form/reaction"

const [values,valuesSetter] = useState({
    name: "",
    age: "",
});


const Name = useField(
  placeholder("hello👋"),
  key("name"),
  component(Input),
  value(values=>values.name),
  onInput((text,setter)=>setter(values=>({
    ...values,
    name:text
  }))),
  props({}),
  style({ }),
  className("")
);

const Age = useField(
  placeholder("hello👋"),
  key("name"),
  component(Input),
  value(values=>values.age),
  onInput((text,setter)=>setter(values=>({
    ...values,
    age:JSON.parse(text)
  }))),
  props({type:'number'}),
  style({}),
  className("")
);

/**
* when typed name "Jack" , age trun to '20'
*/

const reaction = reaction(
  when(Name, or([
      compose(eq("Jack"), props("value")),
      compose(eq(0), JSON.parse, props("value"))
    ])),
  then(Age, 
    value('20')
  )
);

/**
 * when typed Age 22 or 23 , nage trun to 'Terry'
 */
const reaction = reaction(
  when(Age, or([
      compose(eq(22), props("value")),
      compose(eq(23), props("value")),
    ])),
  then(Name, 
    value('Terry')
  )
);

const Form = createForm(Name, Age, reaction);

return <Form values={values} onChange={valuesSetter}></Form>;
  

```
