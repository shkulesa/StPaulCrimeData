<script>
import $ from 'jquery'

export default {
    data() {
        return {
            view: 'map',
            codes: [],
            neighborhoods: {1:'Conway/Battlecreek/Highwood',2:'Greater East Side', 3:'West Side', 4:'Daytons Bluff',
        5:'Payne/Phalen',6:'North End',7:'Thomas/Dale(Frogtown)', 8:'Summit/University', 9:'West Seventh', 10:'Como', 
        11:'Hamline/Midway', 12:'St. Anthony', 13:'Union Park', 14:'Macalester-Groveland', 15:'Highland', 
        16:'Summit Hill', 17:'Capitol River'},
            incidents: [],
            leaflet: {
                map: null,
                center: {
                    lat: 44.955139,
                    lng: -93.102222,
                    address: ""
                },
                zoom: 12,
                bounds: {
                    nw: {lat: 45.008206, lng: -93.217977},
                    se: {lat: 44.883658, lng: -92.993787}
                },
                neighborhood_markers: [
                    {location: [44.942068, -93.020521], marker: null, neighborhood_name:'Conway/Battlecreek/Highwood'},
                    {location: [44.977413, -93.025156], marker: null, neighborhood_name:'Greater East Side'},
                    {location: [44.931244, -93.079578], marker: null, neighborhood_name:'West Side'},
                    {location: [44.956192, -93.060189], marker: null, neighborhood_name:'Daytons Bluff'},
                    {location: [44.978883, -93.068163], marker: null, neighborhood_name:'Payne/Phalen'},
                    {location: [44.975766, -93.113887], marker: null, neighborhood_name:'North End'},
                    {location: [44.959639, -93.121271], marker: null, neighborhood_name:'Thomas/Dale(Frogtown)'},
                    {location: [44.947700, -93.128505], marker: null, neighborhood_name:'Summit/University'},
                    {location: [44.930276, -93.119911], marker: null, neighborhood_name:'West Seventh'},
                    {location: [44.982752, -93.147910], marker: null, neighborhood_name:'Como'},
                    {location: [44.963631, -93.167548], marker: null, neighborhood_name:'Hamline/Midway'},
                    {location: [44.973971, -93.197965], marker: null, neighborhood_name:'St. Anthony'},
                    {location: [44.949043, -93.178261], marker: null, neighborhood_name:'Union Park'},
                    {location: [44.934848, -93.176736], marker: null, neighborhood_name:'Macalester-Groveland'},
                    {location: [44.913106, -93.170779], marker: null, neighborhood_name:'Highland'},
                    {location: [44.937705, -93.136997], marker: null, neighborhood_name:'Summit Hill'},
                    {location: [44.949203, -93.093739], marker: null, neighborhood_name:'Capitol River'}
                ]
            },
            currentAddress: '',
            currentMarker: null,
            inputError: false,
            currentBoundingBox: {},
        };
    },
    methods: {
        viewMap(event) {
            this.view = 'map';
        },

        viewNewIncident(event) {
            this.view = 'new_incident';
        },

        viewAbout(event) {
            this.view = 'about';
        },

        getJSON(url) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    dataType: 'json',
                    url: url,
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({status: status.status, message: status.statusText});
                    }
                });
            });
        },
        uploadJSON(method, url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    type: method,
                    url: url,
                    contentType: 'application/json; charset=utf-8',
                    data: JSON.stringify(data),
                    dataType: 'text',
                    success: (response) => {
                        resolve(response);
                    },
                    error: (status, message) => {
                        reject({status: status.status, message: status.statusText});
                    }
                });
            });
        },
        clearMarkers() {
            $('.leaflet-marker-icon.leaflet-zoom-animated.leaflet-interactive:not(".huechange")').remove();
            $(".leaflet-popup").remove();
            // $(".leaflet-pane.leaflet-shadow-pane").remove();
        },
        isInBoundingBox(lat, lon) {
            return lat >= this.leaflet.bounds.se.lat && lat <= this.leaflet.bounds.nw.lat && lon >= this.leaflet.bounds.nw.lng && lon <= this.leaflet.bounds.se.lng;
        },
        isInBounds(lat, lon, currentBounds) {
            console.log(currentBounds);
            let se = currentBounds._southWest
            let nw = currentBounds._northEast
            return lat >= se.lat && lat <= nw.lat && lon >= se.lng && lon <= nw.lng;
        },
        onInput(e) {
            this.currentAddress = e.target.value;
        },
        onSubmit() {
            this.inputError = false;
            this.getJSON(`https://nominatim.openstreetmap.org/search?q=${encodeURI(this.currentAddress)}&format=json`).then((result) => {
                const {lat, lon} = result[0];
                if(this.isInBoundingBox(lat, lon)) {
                    this.clearMarkers();
                    this.currentMarker = L.marker([lat, lon]).addTo(this.leaflet.map);
                    this.leaflet.map.panTo([lat, lon]);
                } else {
                    this.inputError = true;
                }
            }).catch((error) => {
                console.log(error);
            })
        },
        onInteract() {
            this.inputError = false;
            const currentCenter = this.leaflet.map.getCenter().lat + ',' + this.leaflet.map.getCenter().lng;
            this.getJSON('https://nominatim.openstreetmap.org/search?q=' + currentCenter + '&format=json').then((result) => {
                this.currentAddress = result[0].display_name;
                this.currentBoundingBox = this.leaflet.map.getBounds();
            }).catch((error) => {
                console.log(error);
            });
            this.getJSON('http://localhost:8000/incidents').then((results) => {
            // crime data
            results.sort((inc1,inc2) => new Date(inc2.date_time) - new Date(inc1.date_time));
            results.filter((incident) => {
                return this.isInBounds(this.leaflet.neighborhood_markers[incident.neighborhood_number-1].location[0], this.leaflet.neighborhood_markers[incident.neighborhood_number-1].location[1], this.currentBoundingBox);
            
            });
            this.incidents = results;
            console.log(results);
        }).catch((error) => {
            console.log('Error', error);
        });
        }
    },
    mounted() {
        this.leaflet.map = L.map('leafletmap').setView([this.leaflet.center.lat, this.leaflet.center.lng], this.leaflet.zoom);

        this.currentMarker = L.marker([this.leaflet.center.lat, this.leaflet.center.lng]).addTo(this.leaflet.map);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
            minZoom: 11,
            maxZoom: 18
        }).addTo(this.leaflet.map);
        this.leaflet.map.setMaxBounds([[44.883658, -93.217977], [45.008206, -92.993787]]);

        this.leaflet.map.on('zoomend', this.onInteract);
        this.leaflet.map.on('moveend', this.onInteract);

        let district_boundary = new L.geoJson();
        district_boundary.addTo(this.leaflet.map);

        this.getJSON('/data/StPaulDistrictCouncil.geojson').then((result) => {
            // St. Paul GeoJSON
            $(result.features).each((key, value) => {
                district_boundary.addData(value);
            });
        }).catch((error) => {
            console.log('Error:', error);
        });
<<<<<<< HEAD
        
        this.leaflet.neighborhood_markers.forEach((neighborhood) => {
            neighborhood.marker = L.marker(neighborhood.location).addTo(this.leaflet.map);
            neighborhood.marker._icon.classList.add("huechange");
        })

        $(".leaflet-pane.leaflet-shadow-pane").remove();

=======

        this.getJSON('http://localhost:8000/incidents').then((results) => {
            // crime data
            results.sort((inc1,inc2) => new Date(inc2.date_time) - new Date(inc1.date_time));
            results.filter((incident) => {
                return this.isInBoundingBox(this.leaflet.neighborhood_markers[incident.neighborhood_number-1].location[0], this.leaflet.neighborhood_markers[incident.neighborhood_number-1].location[1]);
            
            });
            this.incidents = results;
            console.log(results);
        }).catch((error) => {
            console.log('Error', error);
        });
>>>>>>> origin/chris
    }
}
</script>

<template>
    <div class="grid-container">
        <div class="grid-x grid-padding-x">
            <p :class="'cell small-4 ' + ((view === 'map') ? 'selected' : 'unselected')" @click="viewMap">Map</p>
            <p :class="'cell small-4 ' + ((view === 'new_incident') ? 'selected' : 'unselected')" @click="viewNewIncident">New Incident</p>
            <p :class="'cell small-4 ' + ((view === 'about') ? 'selected' : 'unselected')" @click="viewAbout">About</p>
        </div>
    </div>
    <div v-show="view === 'map'">
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <form @submit.prevent="onSubmit" class="cell auto" style="padding: 0;" data-abide>
                    <div v-show="inputError === true" data-abide-error class="alert callout" aria-live="assertive" role="alert" style="display: block;">
                        <p><i class="fi-alert"></i>Location is either invalid or not in bound.</p>
                    </div>
                    <div class="input-group">
                    <input :value="currentAddress" @input="onInput" class="input-group-field" type="text" placeholder="Search by Location">
                    <div class="input-group-button">
                        <input type="submit" class="button" value="Go">
                    </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
    <div v-show="view === 'map'">
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <div id="leafletmap" class="cell auto"></div>
            </div>
        </div>
    </div>
    <table>
        <thead>
            <tr>
                <th>#</th>
                <th>Neighborhood</th>
                <th>Incident Type</th>
            </tr>
        </thead>
        <tbody>
            
            <tr v-for="(item, index) in incidents">
                <td>{{ index + 1 }}</td>
                <td>{{ neighborhoods[item.neighborhood_number] }}</td>
                <td>{{ item.incident}}</td>
            </tr>
        </tbody>
    </table>
    <div v-if="view === 'new_incident'">
        <!-- Replace this with your actual form: can be done here or by making a new component -->
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <h1 class="cell auto">New Incident Form</h1>
            </div>
        </div>
    </div>
    <div v-if="view === 'about'">
        <!-- Replace this with your actual about the project content: can be done here or by making a new component -->
        <div class="grid-container">
            <div class="grid-x grid-padding-x">
                <h1 class="cell auto">About the Project</h1>
            </div>
        </div>
    </div>
</template>

<style>
#leafletmap {
    height: 500px;
}

.selected {
    background-color: rgb(10, 100, 126);
    color: white;
    border: solid 1px white;
    text-align: center;
    cursor: pointer;
}
.unselected {
    background-color: rgb(200, 200, 200);
    color: black;
    border: solid 1px white;
    text-align: center;
    cursor: pointer;
}
img.huechange { 
    filter: hue-rotate(120deg); 
}
</style>
