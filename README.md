# withScreenBase (Higher-Order Components)
embed components
1. screen loading component
2. modal alert component

# Step-By-Step
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
# Available props (Push all props into object)
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
# Implement with Redux (reccomment)
**In App folder go to Redux/Types folder then looking for modal.js file you will see modal types**\
```Javascript
export const OPEN_MODAL = 'OPEN_MODAL';
export const CLOSE_MODAL = 'CLOSE_MODAL';
```
**In App folder go to Redux/Actions folder then looking for modal.js file you will see modal actions**\
```Javascript
import * as modalTypes from '../Types/modal';

export const openModal = (payload) => async dispatch => {
    dispatch({
        type: modalTypes.OPEN_MODAL,
        payload: payload
    });
}

export const closeModal = (payload) => async dispatch => {
    dispatch({
        type: modalTypes.CLOSE_MODAL,
        payload: payload
    });
}
```
**In App folder go to Redux/Reducers folder then looking for modal.js file you will see modal reducer**
```Javascript
import * as modalTypes from '../Types/modal';

const initailState = {
    isVisible: false,
    iconType: null,
    textTitleYesNo: null,
    longButton: null,
    title: '',
    subTitle: '',
    body: '',
    onPressPositive: null,
    onPressNegative: null,
    positiveButtonTitle: '',
    negativeButtonTitle: '',
}

export default (state = initailState, action) => {
    const { type, payload } = action;

    switch (type) {
        case modalTypes.OPEN_MODAL:
            return {
                ...state,
                isVisible: true,
                iconType: payload.iconType,
                textTitleYesNo: payload.textTitleYesNo,
                longButton: payload.longButton,
                title: payload.title,
                subTitle: payload.subTitle,
                body: payload.body,
                onPressPositive: () => payload.onPressPositive(),
                onPressNegative: () => payload.onPressNegative(),
                positiveButtonTitle: payload.positiveButtonTitle,
                negativeButtonTitle: payload.negativeButtonTitle
            }
        case modalTypes.CLOSE_MODAL:
            return {
                ...initailState
            }
        default:
            return state;
    }
}
```
# At this point, you should now be able to see the relevant files.
**Go Go Go let's go***
```Javascript
import React from 'react';
import withScreenBase from '../../HOC/with-base/with-base';
import { connect } from 'react-redux';
import { openModal, closeModal } from '../../Redux/Actions/modal';

export const ElseComponent = (props) => {
  const {isScreenLoading, modal, openModal, closeModal} = props;
  
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
  
  const onPressSomeButton = () => {
    openModal(modalProps);
  }
  
  const onPressPositive = () => {
    // do something
    closeModal();
  }
  
  const onPressNegative = () => {
    closeModal();
  }
  
  const HulaComponent = () => {
     return (
       <SomeComponent />
     );
  }
  const WrappedToScreenBase = withScreenBase(HulaComponent);
  
  return(
   <WrappedToScreenBase 
     isScreenLoading={true}/>
  );
  // delete  modalProps={modalProps}
}

const mapStateToProps = state => {
  return {
    isScreenLoading: state.some.loading,
    modal: state.modal
  };
}

const mapDispatchToProps = dispatch => {
  return {
    openModal: (modalProps) => dispatch(openModal(modalProps)),
    closeModal: () => dispatch(closeModal()),
  }
}

export const ElseScreen = connect(mapStateToProps, mapDispatchToProps)(ElseComponent);
```
# Call Redux modal state outside component and call navigation with NavigationService (recomment)
*NavigationService is a function for access to use react-navigation. Yahhh!! now we can use navigation everywhere.\
**Example**

```Javascript
import NavigationService from '../../Navigation/NavigationService';
import { openModal, closeModal } from '../../Redux/Actions/modal';

export const someActionFunction = () => async dispatch => {
   
   const modalProps = {
        iconType: 'warning',
        title: 'การแจ้งเตือน',
        body: 'เกิดข้อผิดพลาดกรุณาลองใหม่อีกครั้งเข้าใจไหม xxx',
        onPressPositive: () => {
            dispatch(closeModal());
            NavigationService.navigate('elseRoute);
        },
        onPressNegative: () => dispatch(closeModal())
   }
   dispatch(openModal(modalProps));
}




```
**Go Go now we finished**



