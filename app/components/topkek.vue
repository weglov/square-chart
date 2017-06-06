<template>
  <div class='modal'>
    <h1>TOP 50:</h1>
    <table>
      <tr v-for='(item,index) in users'>
        <td class='index'>{{index + 1}}.</td><td>{{item._id}} </td><td><strong>{{ item.count }}</strong></td>
        </tr>
      </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      users: [{"_id":"ivan@...","count":2188478115},{"_id":"burik666@...","count":1517206656},{"_id":"256@...","count":748869970},{"_id":"alarkin@...","count":534157110},{"_id":"odn@...","count":492150131},{"_id":"i@...","count":464746509},{"_id":"perminoff@...","count":219648346},{"_id":"ra.bondarenko@...","count":189476616},{"_id":"msalnikov@...","count":109019882},{"_id":"malchenko.dmitriy.by@...","count":105214169},{"_id":"A1977494@...","count":101124294},{"_id":"mbelov@...","count":87111154},{"_id":"hack@...","count":60370320},{"_id":"elena@...","count":44642302},{"_id":"superjob@...","count":37691671},{"_id":"alexey.tsikov@...","count":32884356},{"_id":"minkin.andrew@...","count":27437224},{"_id":"alex21021991@...","count":15688880},{"_id":"kostya.keeper@...","count":10887698},{"_id":"sinclair@...","count":4286092},{"_id":"e.tabatsky@...","count":2378014},{"_id":"evgen300@...","count":2372126},{"_id":"nikita.shapovalov@...","count":2309527},{"_id":"v@...","count":2163356},{"_id":"pen<ОЙ!>s@...","count":2100855},{"_id":"serg_sokolov@...","count":2062901},{"_id":"remss22@...","count":1860253},{"_id":"lebedevcommerical@...","count":1605961},{"_id":"ghostlyfox@...","count":1473142},{"_id":"horechek@...","count":1420287},{"_id":"libbkmz.dev@...","count":1381499},{"_id":"mazurkostya93@...","count":1072706},{"_id":"ua3mqj@...","count":963611},{"_id":"dzmitry_t@...","count":940986},{"_id":"art.eltyshev@...","count":622641},{"_id":"adm-srv@...","count":612810},{"_id":"ilya1997@...","count":358619},{"_id":"georgiosafo@...","count":349630},{"_id":"d.kozhokar@...","count":303539},{"_id":"maniaque.ru@...","count":272614},{"_id":"fes1991@...","count":259647},{"_id":"akis99@...","count":151735},{"_id":"bbldzr@...","count":129178},{"_id":"sinied@...","count":116890},{"_id":"Vsuharnikov@...","count":87585},{"_id":"kuznez_grb@...","count":50437},{"_id":"viktor.vladimirovich.solovev@...","count":20333},{"_id":"voronin-anton1@...","count":18568},{"_id":"alekssmirnov@...","count":9306},{"_id":"michael.yavorovsky@...","count":8785}],
    }
  }
}
</script>

<style lang='scss'>
  .modal {
    position: absolute;
    background: #ffffff;
    border: 3vh solid #0054c5;
    color: #000;
    font-size: 2vh;
    width: 94vw;
    z-index: 200;
    top: 0px;
    left: 0;
    text-align: left;
    padding: 5vh;
    box-shadow: 0px 0 150vh 8px #000;
    margin: 3vh 3vw;
    h1 {
      font-weight: bold;
    }
    .index {
      display: inline-block;
      width: 30px;
      padding-right: 20px;
      text-align: right;
      font-weight: bold;
      color: brown;
    }
  }
</style>