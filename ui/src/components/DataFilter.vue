<template>
    <!-- <div class="grid-container"> -->
    <!-- <div class="x-grid"> -->
    <div class="filter">
      <button class="button" type="button" data-toggle="data-filter">Filter</button>
      <div class="dropdown-pane form cell-auto" id="data-filter" data-dropdown data-auto-focus="true">
        <h4>Filter results</h4>
        <form>
            <div class="grid-container">
                <div class="grid-x grid-padding-x">
                    <div class="cell small-6">
                        <h6>Neighborhood:</h6>
                        <template v-for="(value, key) in neighborhoods">
                            <input type="checkbox" :id=value :value=key v-model="settings.neighborhoods">
                            <label :for=value>{{value}}</label>
                            <br/>
                        </template>
                    </div>
                    <div class="cell small-6">
                        <h6>Incident Type:</h6>
                        <template v-for="(value, key) in type_groups">
                            <input type="checkbox" :id=key :value=key v-model="settings.types">
                            <label :for=key>{{key}}</label>
                            <br/>
                        </template>
                    </div>
                </div>
            </div>
            <h6>Timespan:</h6>
                <div class="grid-x">
                    <div class="small-3 filterDateTime">
                        Start: <input type="date" v-model="settings.start_date">
                    </div>
                    <div class="small-3 filterDateTime">
                        End: <input type="date" v-model="settings.end_date">
                    </div>
                </div>
                <div class="grid-x">
                    <div class="small-3 filterDateTime">
                        <input type="time" v-model="settings.start_time">
                    </div>
                    <div class="small-3 filterDateTime">
                        <input type="time" v-model="settings.end_time">
                    </div>
                </div>
             <h6>Number of Incidents:</h6>
             <div class="grid-x">
                <div class="small-2">
                    <input type="number" min="1" max="10000" v-model="limit">  
                </div>
            </div>
        </form>
        DELETE AFTER TESTING<br/>
        Types: {{settings.types}}<br/>
        Hoods: {{settings.neighborhoods}}<br/>
        Starting from:  {{settings.start_time}}, {{ settings.start_date }} to {{settings.end_time}}, {{ settings.end_date }}<br/>
        {{ settings.limit }} incidents
      </div>
    </div>
</template>

<script>
export default {
    mounted() {
        this.data_filter = new Foundation.Dropdown($('#data-filter'), {
            vOffset: 5
        });
        // this.settings.start_date = this.getDate();
    },
    data() {
        return {
            settings: {
                types: [],
                neighborhoods: [],
                start_date: "",
                end_date: "",
                start_time: "",
                end_time: "",
                limit: ""
            },
            neighborhoods: {1:'Conway/Battlecreek/Highwood', 2:'Greater East Side', 3:'West Side', 4:'Daytons Bluff', 5:'Payne/Phalen',6:'North End',7:'Thomas/Dale(Frogtown)', 8:'Summit/University', 9:'West Seventh', 10:'Como', 11:'Hamline/Midway', 12:'St. Anthony', 13:'Union Park', 14:'Macalester-Groveland', 15:'Highland', 16:'Summit Hill', 17:'Capitol River'},
            type_groups: {
                "Murder": [100, 110, 120],
                "Rape" : [210, 220],
                "Robbery": [300, 311, 312, 313, 314, 321, 322, 323, 324, 331, 333, 334, 341, 342, 343, 344, 351, 352, 353, 354, 361, 363, 364, 371, 372, 373, 374],
                "Assault": [ 400, 410, 411, 412, 420, 421, 422, 430, 431, 432, 440, 441, 442, 450, 451, 452, 453, 810, 861, 862, 863],
                "Burglary": [500, 510, 511, 513, 515, 516, 520, 521, 523, 525, 526, 530, 531, 533, 535, 536, 540, 541, 543, 545, 546, 550, 551, 553, 555, 556, 560, 561, 563, 565, 566],
                "Theft": [600, 603, 611, 612, 613, 614, 621, 622, 623, 630, 631, 632, 633, 640, 641, 642, 643, 651, 652, 653, 661, 662, 663, 671, 672, 673, 681, 682, 683, 691, 692, 693],
                "Motor Vehicle Theft": [700, 710, 711, 712, 720, 721, 722, 730, 731, 732],
                "Arson": [900, 901, 903, 905, 911, 913, 915, 921, 922, 923, 925, 931, 933, 941, 942, 951, 961, 971, 972, 975, 981, 982],
                "Vandalism": [1400, 1401, 1410, 1415, 1416, 1420, 1425, 1426, 1430, 1435, 1436],
                "Narcotics": [1800, 1810, 1811, 1812, 1813, 1814, 1815, 1820, 1822, 1823, 1824, 1825, 1830, 1835, 1840, 1841, 1842, 1843, 1844, 1845, 1850, 1855, 1860, 1865, 1870, 1880, 1885],
                "Other": [2619, 3100, 9954, 9959, 9986]
            }
        }
    }
}
</script>

<style >
    .filter {
        margin-top: .5rem;
    }
    .form {
        width: 80%;
        margin: 1rem;
    }
    .filterDateTime {
        margin-right: 2.5%;
    }
    h6 {
        font-weight: bold;
    }
</style>