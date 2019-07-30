
## npm-package-base

### Manual Installation Through Package Managers

npm package managers

    npm install @team-decorate/select-tiles
    
### Usage

Plugin install:

    import Vue from 'vue'
    import SelectTiles from '@team-decorate/select-tiles'
    
    Vue.use(SelectTiles)

Or work on a Vue instance:


    <select-tiles
          name="test"
          :items="items"
          v-model="selected"
          :old="[]">
          
              <template slot="label">
          　　　　<span>*</span>checkbox
          　　</template>
      </select-tiles>

```
<script>
    import SelectTiles from '@team-decorate/select-tiles'

    export default {
        data() {
            return {
                items: [
                    {id:1, value: 'test1'},
                    {id:2, value: 'test2'},
                    {id:3, value: 'test3'},
                    {id:4, value: 'test4'},
                    {id:5, value: 'test5'},
                ],
                selected: [],
            }
        },
        components: {
            SelectTiles,
        }
    }

</script>
```


    
### Props

|name|type|default|description|
| ---- | ---- | ---- | ---- |
|name|String|---|input name|
|items|Array|required: true|element list|
|mode|String|'checkbox'|change input type 'checkbox' or 'radio'|
|text-key|String|'value'|key for displaying text|
|id-key|---|'id'|Change items id key|
|value-key|---|'value'|Change items value key|
|inputShow|Boolean|false|input hidden status|
|old|Array|[]|initial value|


### Slot
    <slot name='label><span>※</span>checkbox!</slot>
or
    
    <template slot="label">
        <span>*</span>checkbox
    </template>


###Change items key

```html
<select-tiles
      name="test2"
      :items="items"
      v-model="selected2"
      value-key="name"
      text-key="name"
      :old="['test1']"
>
</select-tiles>
```

```html
<script>
    export default {
        data() {
            return {
                items: [
                    {id:1, name: 'user1'},
                    {id:2, name: 'user2'},
                    {id:3, name: 'user3'},
                ],
                selected2: [],
            }
        },
    }

</script>
```

### scss
```scss
.select-tiles {

    &__title {
    
    }
    
    &__label {
      margin-right: 10px;
    }
    //check時
    .select-tiles__input:checked + .select-tiles__btn {
      border-color: red;
      color: red;
    }
    //default時
    &__btn {
      padding: 3px 7px;
      border-radius: 5px;
      border: 1px solid #909090;
      color: #909090;
    }
}

```