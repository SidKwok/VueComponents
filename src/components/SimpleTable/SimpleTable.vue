<template lang="html">
    <div id="crab-table">
        <input type="text" v-model="searchText" />
        <table>
            <thead>
                <tr @click="sort">
                    <td v-for="title in options.titles" :data-sortcol="$index" data-sorttype="desc">
                        {{ title.name }}
                    </td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in currentData">
                    <td v-for="item in row">
                        {{ item }}
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="pagenation" @click="switchPage">
            <a href="javascript: void(0);" :data-page="page - 1">&lt;</a>
            <a href="javascript: void(0);" :data-page="i + 1" v-for="i in allPages">{{ i + 1 }}</a>
            <a href="javascript: void(0);" :data-page="page + 1">&gt;</a>
        </div>
    </div>
</template>

<script>
    /**
     * get the calculated value
     * @param  {String, Number} o - the object you need to calculate
     * @return {Object}   it contains value and the tag
     */
    let calculateObjectValue = o => {
        let obj = {
            val: '0',
            isAnyString: false
        };
        let arr = [];
        let strCount = 0;
        if (typeof o === 'number') {
            o += '';
        }

        if (typeof o === 'string') {
            arr = o.split('').filter(function (item, index) {
                if (Number.isInteger(parseInt(item))) {
                    return true;
                } else {
                    obj.isAnyString = true;
                    return false;
                }
            });

            if (!arr.length) {
                for (let i = 0; i < o.length; i++) {
                    strCount += o.charCodeAt(i);
                }
                obj.val = strCount + '';
                obj.isAnyString = false;
            } else {
                obj.val = arr.join('');
            }
        }

        return obj;
    };

    /**
     * core sort algorithm
     * @param  {String, Number} a   - each data
     * @param  {String, Number} b   - each data
     * @param  {Number} col - which col
     * @param  {String} sortType - type of sort
     * @return {Number} 比较结果
     */
    let sortAlgorithm = (a, b, col, sortType) => {
         let aa = calculateObjectValue(a[col]),
             bb = calculateObjectValue(b[col]),
             length = aa.val.length > bb.val.length ? aa.val.length : bb.val.length,
             gap = 0;

         if (aa.isAnyString || bb.isAnyString) {
             for (let i = 0; i < length; i++) {
                 if (parseInt(aa.val[i]) > parseInt(bb.val[i])) {
                     gap = 1;
                     break;
                 }
                 if (parseInt(aa.val[i]) < parseInt(bb.val[i])) {
                     gap = -1;
                     break;
                 }
             }
         } else {
             gap = parseInt(aa.val) - parseInt(bb.val);
         }

         gap = (sortType === 'desc') ? gap : -gap;
         return gap;
     };

    export default {
        data() {
            return {
                searchText: '',
                page: 1
            }
        },
        props: {
            options: {
                type: Object,
                default() {
                    return {
                        titles: [],
                        sortCols: [],
                        data:[]
                    }
                }
            }
        },
        computed: {
            searchData() {
                return (this.searchText)
                    ? this.search(this.options.data, this.searchText)
                    : this.options.data;
            },
            currentData() {
                return this.searchData.slice((this.page - 1) * 10, this.page * 10);
            },
            allPages() {
                return Math.ceil(this.searchData.length / 10);
            }
        },
        methods: {
            search(rows, searchText) {
                let result = [];
                for (let row of rows) {
                    for (let item of row) {
                        if (('' + item).toLowerCase().includes(searchText)) {
                            result.push(row);
                            break;
                        }
                    }
                }
                return result;
            },
            switchPage(event) {
                let targetPage = parseInt(event.target.dataset.page);
                if (targetPage <= this.allPages && targetPage > 0) {
                    this.page = targetPage;
                }
            },
            sort(event) {
                let col = parseInt(event.target.dataset.sortcol);
                let sortType = event.target.dataset.sorttype;
                if (col !== NaN) {
                    this.options.data.sort(function (a, b) {
                        return sortAlgorithm(a, b, col, sortType);
                    });
                    event.target.dataset.sorttype = (sortType === 'desc') ? 'asc' : 'desc'
                }
            }
        }
    }
</script>

<style lang="css" scoped>
</style>
