## &lt;actindo-combobox&gt;
`actindo-combobox` is a wrapper of the paper-dropdown-menu adding features like filtering, remote data loading, deselecting...

## Example
### use local data
```
<dom-module id="your-element">
    <template>
        <actindo-combobox
            items="[[items]]"
            display-field="value"
            value-field="key"
            value="{{selectedValue}}"
            selected-item="{{selectedItem}}"
            searchable
            allow-deselect
            render="[[render]]
        >
        </actindo-combobox>
    </template>
    <script>
    class YourElement extends Polymer.Element {
        static get is() { return 'your-element';}
        static get properties() {
            return {
                render: {
                    type: Function,
                    value: function() {
                        return function(item) {
                            return "My Value:"+item.value
                        }
                    }
                },
                items: {
                    type: Array,
                    value: function() {return [
                        {key: "key1", value: "value1"},
                        {key: "key2", value: "value2"},
                    ];}
                },
                selectedValue: {
                    type: String
                },
                selectedItem: {
                    type: Object
                }
            }
        }
    }
    customElements.define( YourElement.is, YourElement );
    </script>
</dom-module> 
```
The value field of the selected item will be stored in selected-value while the whole item is stored in selected-item.  
The display field's value is shown per item.  
The optional render function gives the developer flexibility in defining how the items are displayed.  

### use remote data

When setting *remote* the combobox will load the data from remote supporting pagination and remote filtering.

```
<dom-module id="your-element">
    <template>
        <actindo-combobox
            remote="/yourUrl"
            params="[[params]]"
            display-field="value"
            value-field="key"
            value="{{selectedValue}}"
            selected-item="{{selectedItem}}"
            items-per-page="25"
            remote-search
            auto-load
            searchable
            allow-deselect
            render="[[render]]
        >
        </actindo-combobox>
    </template>
    <script>
    class YourElement extends Polymer.Element {
        static get is() { return 'your-element';}
        static get properties() {
            return {
                render: {
                    type: Function,
                    value: function() {
                        return function(item) {
                            return "My Value:"+item.value
                        }
                    }
                },
                params: {
                    type: Object,
                    value: function() {
                        return {param1: "param1", param2: "param2"}
                    }
                },
                selectedValue: {
                    type: String
                },
                selectedItem: {
                    type: Object
                }
            }
        }
    }
    customElements.define( YourElement.is, YourElement );
    </script>
</dom-module> 
```
