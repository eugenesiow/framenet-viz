<template>
   <div class="container">
     <q-item>
       <q-item-section>
          <q-input
            v-model="sentence"
            filled
            type="textarea"
          />
       </q-item-section>
     </q-item>
     <q-item>
       <q-item-section>
        <q-list bordered separator>
            <q-markup-table>
              <thead>
                <tr>
                  <th class="text-center" v-for="row in getSentenceHeader(sentence)" :key="row.id">{{ row.name }}</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="row in getSentenceTable(sentence)" :key="row.id">
                  <td class="text-right">{{ row.name }}</td>
                  <td :class="getCSS(col.type)" v-for="col in filterSpans(row.frames)" :key="col.idx" :rowspan="col.span">
                    <span v-if="col.type !== 0">{{ col.name }}</span>
                  </td>
                </tr>
              </tbody>
            </q-markup-table>  
        </q-list>
       </q-item-section>
     </q-item>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      sentence: "{ \"frames\": [ { \"target\": { \"name\": \"Age\", \"spans\": [ { \"start\": 1, \"end\": 2, \"text\": \"young\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 38.21858929902089, \"frameElements\": [ { \"name\": \"Entity\", \"spans\": [ { \"start\": 2, \"end\": 3, \"text\": \"PAP\" } ] } ] } ] }, { \"target\": { \"name\": \"Taking_sides\", \"spans\": [ { \"start\": 3, \"end\": 4, \"text\": \"supporter\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 50.60650531905142, \"frameElements\": [] } ] }, { \"target\": { \"name\": \"Statement\", \"spans\": [ { \"start\": 4, \"end\": 5, \"text\": \"tells\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 102.50487778253861, \"frameElements\": [ { \"name\": \"Message\", \"spans\": [ { \"start\": 6, \"end\": 34, \"text\": \"why they still firmly believe in the PAP , even as , amongst their social circles , it has become `` unfashionable '' to publicly support the party\" } ] }, { \"name\": \"Speaker\", \"spans\": [ { \"start\": 0, \"end\": 4, \"text\": \"A young PAP supporter\" } ] } ] } ] }, { \"target\": { \"name\": \"Reason\", \"spans\": [ { \"start\": 6, \"end\": 7, \"text\": \"why\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 10.10532304361336, \"frameElements\": [] } ] }, { \"target\": { \"name\": \"Continued_state_of_affairs\", \"spans\": [ { \"start\": 8, \"end\": 9, \"text\": \"still\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 15.432040109829346, \"frameElements\": [ { \"name\": \"State_of_affairs\", \"spans\": [ { \"start\": 7, \"end\": 8, \"text\": \"they\" } ] }, { \"name\": \"Reference_occasion\", \"spans\": [ { \"start\": 8, \"end\": 9, \"text\": \"still\" } ] } ] } ] }, { \"target\": { \"name\": \"Awareness\", \"spans\": [ { \"start\": 10, \"end\": 11, \"text\": \"believe\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 57.37169898865221, \"frameElements\": [ { \"name\": \"Content\", \"spans\": [ { \"start\": 11, \"end\": 14, \"text\": \"in the PAP\" } ] }, { \"name\": \"Cognizer\", \"spans\": [ { \"start\": 7, \"end\": 8, \"text\": \"they\" } ] }, { \"name\": \"Degree\", \"spans\": [ { \"start\": 9, \"end\": 10, \"text\": \"firmly\" } ] } ] } ] }, { \"target\": { \"name\": \"Social_event\", \"spans\": [ { \"start\": 20, \"end\": 21, \"text\": \"social\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 64.76364741705271, \"frameElements\": [ { \"name\": \"Social_event\", \"spans\": [ { \"start\": 21, \"end\": 22, \"text\": \"circles\" } ] } ] } ] }, { \"target\": { \"name\": \"Aggregate\", \"spans\": [ { \"start\": 21, \"end\": 22, \"text\": \"circles\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 31.561540478383133, \"frameElements\": [ { \"name\": \"Aggregate\", \"spans\": [ { \"start\": 21, \"end\": 22, \"text\": \"circles\" } ] }, { \"name\": \"AggregateProperty\", \"spans\": [ { \"start\": 20, \"end\": 21, \"text\": \"social\" } ] } ] } ] }, { \"target\": { \"name\": \"Becoming\", \"spans\": [ { \"start\": 25, \"end\": 26, \"text\": \"become\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 71.97617862166335, \"frameElements\": [ { \"name\": \"Entity\", \"spans\": [ { \"start\": 23, \"end\": 24, \"text\": \"it\" } ] } ] } ] }, { \"target\": { \"name\": \"Secrecy_status\", \"spans\": [ { \"start\": 30, \"end\": 31, \"text\": \"publicly\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 24.294288698672446, \"frameElements\": [ { \"name\": \"Phenomenon\", \"spans\": [ { \"start\": 32, \"end\": 34, \"text\": \"the party\" } ] } ] } ] }, { \"target\": { \"name\": \"Taking_sides\", \"spans\": [ { \"start\": 31, \"end\": 32, \"text\": \"support\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 54.79478840660616, \"frameElements\": [ { \"name\": \"Cognizer\", \"spans\": [ { \"start\": 23, \"end\": 24, \"text\": \"it\" } ] }, { \"name\": \"Side\", \"spans\": [ { \"start\": 32, \"end\": 34, \"text\": \"the party\" } ] } ] } ] }, { \"target\": { \"name\": \"Participation\", \"spans\": [ { \"start\": 33, \"end\": 34, \"text\": \"party\" } ] }, \"annotationSets\": [ { \"rank\": 0, \"score\": 51.70274690331915, \"frameElements\": [] } ] } ], \"tokens\": [ \"A\", \"young\", \"PAP\", \"supporter\", \"tells\", \"us\", \"why\", \"they\", \"still\", \"firmly\", \"believe\", \"in\", \"the\", \"PAP\", \",\", \"even\", \"as\", \",\", \"amongst\", \"their\", \"social\", \"circles\", \",\", \"it\", \"has\", \"become\", \"``\", \"unfashionable\", \"''\", \"to\", \"publicly\", \"support\", \"the\", \"party\", \".\" ] }",
    }
  },
  methods: {
    getCSS(colType) {
      let cssStr = ''
      if (colType === 1) {
        cssStr += 'target-cell'
      } else if (colType === 2) {
        cssStr += 'frame-cell'
      }
      return 'text-center '+ cssStr
    },
    filterSpans (items) {
      return items.filter(function (item) {
        return item.type !== -1
      })
    },
    getSentenceHeader (sentenceStr) {
      const sentence = JSON.parse(sentenceStr)
      const headerRow = [{id: 0, name: ''}]
      const frames = sentence['frames']
      for(let i=0; i< frames.length; i++) {
        headerRow.push({id: 'header'+i, name: frames[i]['target']['name']})
      }
      return headerRow
    },
    getSentenceTable (sentenceStr) {
      const sentence = JSON.parse(sentenceStr)
      const rows = []
      const table = []
      const frames = sentence['frames']
      const tokens = sentence['tokens']
      
      for(let i=0; i<tokens.length; i++) {
        const blankRow = []
        for(let j=0; j<frames.length; j++) {
          blankRow.push({type: 0, name: '', idx: 'record-'+i+'-'+j, span: 1})
        }
        table.push(Array.from(blankRow))
      }
      for(let i=0; i<frames.length; i++) {
        const target = frames[i]['target']
        for(let j=0; j<target['spans'].length; j++) {
          const span = target['spans'][j]
          for(let k=span['start']; k<span['end']; k++) {
            table[k][i].name = target['name']
            table[k][i].type = 1
          }
        }
        for(let j=0; j<frames[i]['annotationSets'].length; j++) {
          const annotationSets = frames[i]['annotationSets']
          for(let k=0; k<annotationSets.length; k++) {
            const frameElements = annotationSets[k]['frameElements']
            for(let l=0; l<frameElements.length; l++) {
              const frameElement = frameElements[l]
              const frameElementName = frameElement['name']
              for(let m=0; m<frameElement['spans'].length; m++) {
                const span = frameElement['spans'][m]
                const diff = span['end']-span['start']
                table[span['start']][i].name = frameElementName
                table[span['start']][i].span = diff
                table[span['start']][i].type = 2
                for(let n=1; n<diff; n++) {
                  table[span['start']+n][i].type = -1
                }
              }
            }
          }
        }
      }
      for(let i=0; i<tokens.length; i++) {
        rows.push({id: 'token'+i, name: tokens[i], frames: table[i]})
      }
      return rows
    }
  }
}
</script>

<style scoped>
  .frame-cell {
    background-color: #cccccc;
  }
  .target-cell {
    background-color: #333333;
    color: #fff;
  }
</style>