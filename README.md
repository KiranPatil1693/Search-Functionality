*****/index.js
import React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import rootReducer from './reducers'
import App from './components/App'
import './App'
const store = createStore(rootReducer)
console.log(store.getState())
render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root'))
*****/App.css
  .SearchGrid {
  display: grid;
  grid-template-columns: 10% 60%;
}
****/actions/index
export const SearchSelectOnChange = SearchSelectValue => {
    console.log(SearchSelectValue)
    return ({type: 'SEARCH_SELECT_ON_CHANGE',
     SearchSelectValue
    })
}
export const SearchSuggestionClick = SearchSuggestionValue => ({
    type: 'SEARCH_SUGGESTION_CLICK',
    SearchSuggestionValue
})
export const SearchGetSuggestions = GetSuggestionsValue => ({
    type: 'SEARCH_GET_SUGGESTIONS',
    GetSuggestionsValue
})
export const SearchSubmit = SearchSubmitValue => ({
    type: 'SEARCH_SUBMIT',
    SearchSubmitValue
})
*****/components/App
import React from 'react'
import SearchSelectContainer from '../containers/SearchSelectContainer'
import SearchTypeContainer from '../containers/SearchTypeContainer'
const App = () => {
	return (
      <div>
        <div>
          <div className="SearchGrid">
            <span><SearchSelectContainer /></span>
            <span><SearchTypeContainer /></span>
          </div>
        </div>
      </div>
	)
} 
export default App
*****/components/SearchSelect
import React from 'react'
const SearchSelect = ({onSelectChange}) => {
		return (
          <span>
            <select onChange={onSelectChange} style={{width:'100%'}}>
              <option  value='All'>All</option>
              <option  value='Cars'>Cars</option>
              <option  value='Mobiles'>Mobiles</option>
              <option  value='Cloths'>Cloths</option>
              <option  value='Diamonds'>Diamonds</option>
            </select>
          </span>
		)
}
export default SearchSelect
*****/components/SearchType
import React from 'react'
const SearchType = ({SearchPlaceholder, GetSuggestionsList}) => {
	return (
      <span>
        <form action='#'>
          <input type='text' placeholder={SearchPlaceholder} onChange={GetSuggestionsList} style={{width:'100%'}} />
        </form>
      </span>
	)
}
export default SearchType
*****/containers/SearchSelectContainer
import React from 'react'
import { connect } from 'react-redux'
import SearchSelect from '../components/SearchSelect'
import { SearchSelectOnChange } from '../actions/index.js' 
const mapStateToProps = state => ({
  SearchSelectValue: state.Search.SearchSelectValue
})
const mapDispatchToProps = dispatch => ({
	onSelectChange: (event) => dispatch(SearchSelectOnChange(event.target.value))
})
export default connect(mapStateToProps, mapDispatchToProps)(SearchSelect)
****/continers/SearchTypeContainer
import React from 'react'
import { connect } from 'react-redux'
import SearchSelect from '../components/SearchSelect'
import { SearchSelectOnChange } from '../actions/index.js' 
const mapStateToProps = state => ({
  SearchSelectValue: state.Search.SearchSelectValue
})
const mapDispatchToProps = dispatch => ({
	onSelectChange: (event) => dispatch(SearchSelectOnChange(event.target.value))
})
export default connect(mapStateToProps, mapDispatchToProps)(SearchSelect)
******/reducers/Search
const Search = (state={SearchSelectValue: 'All',SearchPlaceholder: 'Search in All'},action) => {
    switch (action.type) {
        case 'SEARCH_SELECT_ON_CHANGE':
          return {
          	...state,
            SearchSelectValue: action.SearchSelectValue,
            SearchPlaceholder: `Search in ${action.SearchSelectValue}`  
          }
        default:
          return state
      }
    }
export default Search
******/reducers/index
import { combineReducers } from 'redux'
import Search from '../reducers/Search'
export default combineReducers({
  Search
})
