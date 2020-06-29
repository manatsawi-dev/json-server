# IMPORTANT
**When call navigation or NavigationService after modal dismiss**\
*May be an error with Can't read property 'state' of null*\
*Fix by waiting for the modal state to change*\

```Javascript
import NavigationModalService from '../../utils//navigation-modal-helpers';

const onPressedSomeAction = () => {
    closeModal();
    NavigationModalService.navigate('loggedIn');
}

```

*NavigationModalService*
```Javascript
export const navigate = (routeName) => {
    setTimeout(() => {
        if (routeName) NavigationService.navigate(routeName);
    }, 50);
}
export default NavigationModalService = {
    navigate
}
```

# Available props (Push all props into object)
| Name | Type  | Default  | Description |
| :---:   | :-: | :--- | :--- |
| isVisible | boolean | **REQUIRED** | Show the modal? |
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
