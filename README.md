# withScreenBase (Higher-Order Components)
embed components
1. screen loading component
2. modal alert component

# Step-To-Step
**1. import component withScreenBase**
```Javascript
import withScreenBase from '../../HOC/with-base/with-base';
```
**2. wrap component into withScreenBase**
```Javascript
import React from 'react';
import withScreenBase from '../../HOC/with-base/with-base';

export const ElseComponent = (props) => {
  const HulaComponent = () => {
     return (
       <SomeComponent />
     );
  }
  const WrappedToScreenBase = withScreenBase(HulaComponent);

  return(
   <WrappedToScreenBase/>
  );
}
```
# Screen loading
**How to show screen is loading ?**\
*pass value true if you need to show screen loading or false if you need hide screen loading to isScreenLoading props*
```Javascript
import React from 'react';
import withScreenBase from '../../HOC/with-base/with-base';

export const ElseComponent = (props) => {
  const HulaComponent = () => {
     return (
       <SomeComponent />
     );
  }
  const WrappedToScreenBase = withScreenBase(HulaComponent);

  return(
   <WrappedToScreenBase isScreenLoading={true}/>
  );
}
```
# Awesome alert
**How to show awesome alert ?**\
*pass modalProps into modalProps props
```Javascript
import React from 'react';
import withScreenBase from '../../HOC/with-base/with-base';

export const ElseComponent = (props) => {
  const HulaComponent = () => {
     return (
       <SomeComponent />
     );
  }
  const WrappedToScreenBase = withScreenBase(HulaComponent);
  const modalProps = {}
  return(
   <WrappedToScreenBase 
     isScreenLoading={true}
     modalProps={modalProps}/>
  );
}
```
# Available props (Push all props in to object)
| Name | Type  | Default  | Description |
| :---:   | :-: | :--- | :--- |
| isVisibleModal | boolean | **REQUIRED** | Show the modal? |
| iconType | string | 'warning' | The icon type support one of 'success', 'danger', 'warning', **can be null then will not show icon** |
| title | string | 'การแจ้งเตือน' | Alert title. |
| subTitle | string | null | Alert sub title. **can be null** |
| body | string | null | Alert body. **can be null** |
| buttonYesNo | boolean | null | Change button title to 'ใช่' หรือ 'ไม่ใช่' default is 'ตกลง' และ 'ยกเลิก'. **can be null**
| longButton | boolean | null | Change display button in row to column for long button title. **can be null** |
| onPressPositive | function | **REQUIRED** | Handler function when press positive button |
| onPressNegative | function | null | Handler function when press negative button. **If value is null will not show negative button** |
| positiveButtonTitle | string | null | Long positive button title. **It will trigged when longButton value is true**
| negativeButtonTitle | string | null | Long negative button title. **It will trigged when longButton value is true**

# Completed example
```Javascript
import React from 'react';
import withScreenBase from '../../HOC/with-base/with-base';

export const ElseComponent = (props) => {
  const HulaComponent = () => {
     return (
       <SomeComponent />
     );
  }
  const WrappedToScreenBase = withScreenBase(HulaComponent);
  const modalProps = {
    isVisibleModal: true,
    iconType: 'warning',
    title: 'การแจ้งเตือน',
    body: 'เกิดข้อผิดพลาดกรุณาลองใหม่อีกครั้งเข้าใจไหม',
    longButton: true,
    positiveButtonTitle: 'แสดงอีกครั้งภายหลัง',
    negativeButtonTitle: 'ไม่ต้องแสดงอีก',
    onPressPositive: () => {},// onPressPositiveModal(),
    onPressNegative: () => {}, //onPressCloseModel()
  }
  return(
   <WrappedToScreenBase 
     isScreenLoading={true}
     modalProps={modalProps}/>
  );
}
```
