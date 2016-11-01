# redux-react-i18n
i18n component and reducers for redux

Terminal:
```javascript
npm i 'redux-react-i18n'
```

##Your code (complete solution):
```javascript
import { i18nReducer, i18nActions, Loc } from 'redux-react-i18n';

...
// reducers - is your reducers
reducers.i18n = i18nReducer;
...

const store = createStore( combineReducers( reducers ) );

...
// Set dictionaries (simpliest exapmple) -----------------------------------------------------------------------------------------------

// This dictionaries can be supported by Localization team without need to know somth about interface or project, 
// and you just can fetch it to your project
const dictionaries = {
    'ru-RU': {
        'key_1': 'Первый дефолтный ключ',
        'key_2': [ '$Count', ' ', ['штучка','штучки','штучек']], // 1 штучка, 3 штучки, пять штучек
        /* ... */
        /* Other keys */
    },
    'en-US': {
        'key_1': 'First default key',
        'key_2': [ '$Count', ' ', ['thing','things']], // 1 thing, 2 things, 153 things
    }
    /* ... */
    /* Other dictionaries */
}
store.dispatch( i18nActions.setDictionaries( dictionaries ) );
// / Set dictionaries (simpliest exapmple) ---------------------------------------------------------------------------------------------

// Set languages (simpliest exapmple) --------------------------------------------------------------------------------------------------
const languages = [
    {
        code: 'ru-RU',
        name: 'Русский'
    },
    {
        code: 'en-US',
        name: 'English (USA)'
    }
    /* ... */
    /* Other languages */
];

store.dispatch( i18nActions.setLanguages( languages ) );
// / Set languages (simpliest exapmple) ------------------------------------------------------------------------------------------------

// Set current language code (you can map this action to select component or somth like this)
store.dispatch( i18nActions.setCurrent( 'ru-RU' ) );
```

#### And now inside any component you can use mapped container component

```javascript
import { Loc } from 'redux-react-i18n';
...

<p>
  <Loc locKey="key_1"/> // => Первый дефолтный ключ
</p>

<p>
  <Loc locKey="key_2" number={7}/> // => 7 штучек
</p>
```

##Your code (Just use a dumb component and you can design store/actions/reducers by yourself like you want):

```javascript
// Just import presentational component LocPresentational
import { LocPresentational } from 'redux-react-i18n';
...

// Then map data to props => currentLanguage, dictionary (See more in src/Loc.js):

const mapStateToProps = ( { /*getting data from the state*/ }, ownProps ) => ({
    currentLanguage: yourCurrentLanguageFromState,
    dictionary: yourDictionaryFromState
});
Loc = connect( mapStateToProps )( LocPresentational );

...

<p>
  <Loc locKey="YOUR_KEY_1"/>
</p>

<p>
  <Loc locKey="YOUR_KEY_2"  number={42}/>
</p>
```
See more in src/\*.js
