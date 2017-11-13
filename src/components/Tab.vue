<template>
  <div>
    <div id="lineContent">Contenu de ligne</div>

    <div class="corps">
      
      <div id="result">Tableau</div>
      <button type="button" class="btnoriginal" @click="orderList">Remettre les colonnes dans l'ordre de départ</button>

      <div class="tableau" @scroll="displayBtn">
        <draggable class="externe" element="ul" v-model="list" :options="dragOptions" :move="onMove" @start="isDragging=true" @end="isDragging=false"> 
          <transition-group type="transition" :name="'flip-list'">
            <li v-for="element in list" :key="element.order"> 
              <ul class="interne">
                <li><span @click="trier">{{element.name}}</span></li>
                <li v-for="(message, i) in list2" :key="message.id" @click="colorTarget(i, $event)">{{message[element.name]}}</li>
                <li>{{element.order}}</li>
              </ul>
            </li> 
          </transition-group>
        </draggable>
        <div class="btnbtot1" @click="remonteTab">Remonter en haut du tableau</div>
      </div>

    </div>
    <div class="btnbtot2" @click="remonteTab">Remonter en haut du tableau</div>
  </div>
</template>

<script>
  import draggable from 'vuedraggable';

  const data = [ 
    {id: 0,   auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 1,   auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 2,   auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 3,   auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 4,   auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 5,   auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 6,   auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 7,   auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 8,   auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 9,   auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 10,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
    {id: 11,  auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 12,  auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 13,  auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 14,  auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 15,  auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 16,  auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 17,  auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 18,  auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 19,  auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 20,  auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 21,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
    {id: 22,  auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 23,  auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 24,  auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 25,  auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 26,  auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 27,  auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 28,  auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 29,  auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 30,  auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 31,  auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 32,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
    {id: 33,  auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 34,  auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 35,  auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 36,  auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 37,  auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 38,  auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 39,  auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 40,  auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 41,  auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 42,  auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 43,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
    {id: 44,  auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 45,  auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 46,  auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 47,  auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 48,  auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 49,  auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 50,  auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 51,  auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 52,  auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 53,  auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 54,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
    {id: 55,  auteur: 'thibaut',  ligne: 'ligne 1',   site: 'site1',    colonne1: 'test1',    colonne2: 'test1'}, 
    {id: 56,  auteur: 'megane',   ligne: 'ligne 2',   site: 'site2',    colonne1: 'test2',    colonne2: 'test2'},
    {id: 57,  auteur: 'clovis',   ligne: 'ligne 3',   site: 'site3',    colonne1: 'test3',    colonne2: 'test3'},
    {id: 58,  auteur: 'renaud',   ligne: 'ligne 4',   site: 'site4',    colonne1: 'test4',    colonne2: 'test4'},
    {id: 59,  auteur: 'jean',     ligne: 'ligne 5',   site: 'site5',    colonne1: 'test5',    colonne2: 'test5'},
    {id: 60,  auteur: 'mickael',  ligne: 'ligne 6',   site: 'site6',    colonne1: 'test6',    colonne2: 'test6'},
    {id: 61,  auteur: 'geoffrey', ligne: 'ligne 7',   site: 'site7',    colonne1: 'test7',    colonne2: 'test7'},
    {id: 62,  auteur: 'rose',     ligne: 'ligne 8',   site: 'site8',    colonne1: 'test8',    colonne2: 'test8'},
    {id: 63,  auteur: 'philippe', ligne: 'ligne 9',   site: 'site9',    colonne1: 'test9',    colonne2: 'test9'},
    {id: 64,  auteur: 'kevin',    ligne: 'ligne 10',  site: 'site10',   colonne1: 'test10',   colonne2: 'test10'},
    {id: 65,  auteur: 'josé',     ligne: 'ligne 11',  site: 'site11',   colonne1: 'test11',   colonne2: 'test11'},
  ];

  const columns = Object.keys(data[0]);

  export default {
    name: 'tab',
    components: {
      draggable,
    },
    data () {
      return {
        list: columns.map((name,index) => { return {name, order: index+1, fixed: false}; }),
        list2: data,
        displayContent: '',
        editable: true,
        isDragging: false,
        delayedDragging: false
      }
    },
    methods:{
      orderList () {
        this.list = this.list.sort((one,two) =>{return one.order-two.order; })
      },
      onMove ({relatedContext, draggedContext}) {
        const relatedElement = relatedContext.element;
        const draggedElement = draggedContext.element;
        return (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      },
      colorTarget (key, e) {
        let allLi = document.querySelectorAll('ul.interne li');
        for (let i = 0; i < allLi.length; i++) {
          allLi[i].style.backgroundColor = "";
          allLi[i].style.color = "";
        }
        let ul = document.querySelectorAll('ul.interne');
        let dataContent = [];
        for (let i = 0; i < ul.length; i++) {
          let li = ul[i].querySelectorAll('li');
          li[key+1].style.backgroundColor = "#40E583";
          li[key+1].style.color = "#111111";
          dataContent.push(li[key+1].textContent);
        }
        document.querySelector('#result').textContent = e.target.textContent;
        let cols = document.querySelectorAll('ul.interne li span');
        let displayContent = '';
        for (let d = 0; d < cols.length; d++) {
          displayContent += cols[d].textContent + ': ' + dataContent[d] + '<br>';
        }
        document.querySelector('#lineContent').innerHTML = displayContent;
      },
      trier (e) {
        let spans = document.querySelectorAll('ul.interne li span');
        for (let i = 0; i < spans.length; i++) {
          spans[i].style.color = "";
        }
        let tri = e.target.textContent;
        this.list2 = this.list2.sort((a, b) => {
          if (a[tri] < b[tri]) return -1;
          else if (a[tri] == b[tri]) return 0;
          else return 1;
        });
        e.target.style.color = "#ffffff";
      },
      remonteTab () {
        document.querySelector('.tableau').scrollTo(0, 0);
      },
      displayBtn () {
        if (document.querySelector('.tableau').scrollTop > 10) {
          document.querySelector('.btnbtot2').style.display="block";
        } else {
          document.querySelector('.btnbtot2').style.display="none";
        }
      }
    },
    computed: {
      dragOptions () {
        return  {
          animation: 0,
          group: 'description',
          disabled: !this.editable,
          ghostClass: 'ghost'
        };
      },
      listString(){
        return JSON.stringify(this.list, null, 2);  
      }
    },
    watch: {
      isDragging (newValue) {
        if (newValue){
          this.delayedDragging = true;
          return
        }
        this.$nextTick(() =>{
            this.delayedDragging = false;
        })
      }
    }
  }
</script>

<style scoped>

#lineContent {
  position: fixed;
  top: 40%; left: 20px;
  width: 15%;
  padding: 7px;
  background-color: #333333;
  border: 1px solid black;
  border-radius: 4px;
  color: #40E583;
  font-size: 18px;
  line-height: 30px;
}

  #lineContent span {
    display: block;
    color: #40E583;
  }

.corps {
    position: fixed;
    background-color: #ffffff;
    top: 70px;
    right: 40px;
    width: calc(85% - 80px); height: calc(100% - 130px);
        -moz-box-shadow: 0px 0px 7px 0px #656565;
        -webkit-box-shadow: 0px 0px 7px 0px #656565;
        -o-box-shadow: 0px 0px 7px 0px #656565;
        box-shadow: 0px 0px 7px 0px #656565;
        filter:progid:DXImageTransform.Microsoft.Shadow(color=#656565, Direction=NaN, Strength=7);
}

  #result {
    width: 100%;
    background-color: #40E583;
    border: 0px solid #444444;
    text-align: center;
    font-size: 30px; color: #ffffff;
  }

  .btnoriginal {
    display: block;
    margin: 6px auto 0px;
    padding: 4px 12px;
    background-color: #dddddd;
    border: none;
    border-radius: 4px;
  }

  .tableau {
    margin: 6px auto;
    height: 882px;
    overflow-y: scroll;
  }

  ul.externe span {
    display: flex;
    flex-direction: row;
    flex-flow: row wrap;
    justify-content: center;
  }

  ul.externe span li {
    flex: 1;
    text-align: center;
    list-style: none;
  }

  ul.interne > li {
    border-left: 1px solid #999999;
    border-bottom: 1px solid #999999;
  }

  ul.interne > li:nth-child(even) {
    background-color: #eee;
  }

  ul.interne > li:first-child {
    background-color: #333333;
    color: #40E583; font-size: 18px;
    border-top: 1px solid black;
  }

  ul.interne > li > span {
    font-weight: bold;
  }

  .corps .btnbtot1 {
      background-color: #73a8ee;
      margin: 10px auto;
      width: 300px;
      text-align: center;
      cursor: pointer;
      color: #111111;
      font-size: 14px;
      padding: 7px;
      border-radius: 4px;
  }

  .btnbtot2 {
    display: none;
    position: absolute;
    bottom: 10px; right: 40px;
    background-color: #40E583;
    text-align: center;
    cursor: pointer;
    color: #111111;
    font-size: 14px;
    padding: 7px 18px;
    border-radius: 4px;
  }

  /* ##################################################### */

  .flip-list-move {
    transition: transform 0.5s;
  }

  .no-move {
    transition: transform 0s;
  }

  .ghost {
    opacity: .5;
    background: #C8EBFB;
  }

  ul.externe span li ul.interne li:first-child:hover {
    cursor: grab;
  }

  ul.externe span li ul.interne li:first-child:active {
    cursor: grabbing;
  }

  ul.externe span li ul.interne li:hover {
    background-color: #333333;
    color: #40E583;
    cursor: default;
  }

</style>
