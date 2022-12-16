<script>
    export default {
        data() {
            return {
                data: {
                    case: "",
                    code: "",
                    date: "",
                    time: "",
                    grid: "",
                    type: "",
                    neighborhood: "",
                    block: ""
                },
                nextCaseNumber: 22094836,
                types: {
                    "100":"HOMICIDE",
                    "110":"Murder, Non Negligent Manslaughter",
                    "120":"Murder, Manslaughter By Negligence",
                    "210":"Rape, By Force",
                    "220":"Rape, Attempt",
                    "300":"Robbery",
                    "311":"Robbery, Highway, Firearm",
                    "312":"Robbery, Highway, Knife or Cutting Instrument",
                    "313":"Robbery, Highway, Other Dangerous Weapons",
                    "314":"Robbery, Highway, By Strong Arm",
                    "321":"Robbery, Commercial House, Firearm",
                    "322":"Robbery, Commercial House, Knife or Cutting Instrument",
                    "323":"Robbery, Commercial House, Other Dangerous Weapons",
                    "324":"Robbery, Commercial House, By Strong Arm",
                    "331":"Robbery, Service Station, Firearm",
                    "333":"Robbery, Service Station, Other Dangerous Weapons",
                    "334":"Robbery, Service Station, By Strong Arm",
                    "341":"Robbery, Convenience Store, Firearm",
                    "342":"Robbery, Convenience Store, Knife or Cutting Instrument",
                    "343":"Robbery, Convenience Store, Other Dangerous Weapons",
                    "344":"Robbery, Convenience Store, By Strong Arm",
                    "351":"Robbery, Residence, Firearm",
                    "352":"Robbery, Residence, Knife or Cutting Instrument",
                    "353":"Robbery, Residence, Other Dangerous Weapons",
                    "354":"Robbery, Residence, By Strong Arm",
                    "361":"Robbery, Bank, Firearm",
                    "363":"Robbery, Bank, Other Dangerous Weapons",
                    "364":"Robbery, Bank, By Strong Arm",
                    "371":"Robbery, Misc., Firearm",
                    "372":"Robbery, Misc., Knife or Cutting Instrument",
                    "373":"Robbery, Misc., Other Dangerous Weapons",
                    "374":"Robbery, Misc., By Strong Arm",
                    "400":"Aggravated Assault",
                    "410":"Aggravated Assault, Firearm",
                    "411":"Aggravated Assault, Domestic",
                    "412":"Aggravated Assault, Domestic",
                    "420":"Aggravated Assault, Knife or Cutting Instrument",
                    "421":"Aggravated Assault, Domestic",
                    "422":"Aggravated Assault, Domestic",
                    "430":"Aggravated Assault, Other Dangerous Weapons",
                    "431":"Aggravated Assault, Domestic",
                    "432":"Aggravated Assault, Domestic",
                    "440":"Aggravated Assault, Fists/Feet/Hands",
                    "441":"Aggravated Assault, Domestic",
                    "442":"Aggravated Assault, Domestic",
                    "450":"Aggravated Assault, Domestic",
                    "451":"Aggravated Assault, Domestic",
                    "452":"Aggravated Assault, Domestic",
                    "453":"Aggravated Assault, Domestic",
                    "500":"Burglary",
                    "510":"Burglary, Forced Entry, Night, Residence",
                    "511":"Burglary, Forced Entry, Night, Residence, Occupied",
                    "513":"Burglary, Forced Entry, Night, Garage",
                    "515":"Burglary, Forced Entry, Night, Commercial",
                    "516":"Burglary, Forced Entry, Night, Commercial, Occupied",
                    "520":"Burglary, No Forced Entry, Night, Residence",
                    "521":"Burglary, No Forced Entry, Night, Residence, Occupied",
                    "523":"Burglary, No Forced Entry, Night, Garage",
                    "525":"Burglary, No Forced Entry, Night, Commercial",
                    "526":"Burglary, No Forced Entry, Night, Commercial, Occupied",
                    "530":"Burglary, Forced Entry, Day, Residence",
                    "531":"Burglary, Forced Entry, Day, Residence, Occupied",
                    "533":"Burglary, Forced Entry, Day, Garage",
                    "535":"Burglary, Forced Entry, Day, Commercial",
                    "536":"Burglary, Forced Entry, Day, Commercial, Occupied",
                    "540":"Burglary, No Forced Entry, Day, Residence",
                    "541":"Burglary, No Forced Entry, Day, Residence, Occupied",
                    "543":"Burglary, No Forced Entry, Day, Garage",
                    "545":"Burglary, No Forced Entry, Day, Commercial",
                    "546":"Burglary, No Forced Entry, Day, Commercial, Occupied",
                    "550":"Att. Burglary, Forced Entry, Night, Residence",
                    "551":"Att. Burglary, Forced Entry, Night, Residence, Occupied",
                    "553":"Att. Burglary, Forced Entry, Night, Garage",
                    "555":"Att. Burglary, Forced Entry, Night, Commercial",
                    "556":"Att. Burglary, Forced Entry, Night, Commercial, Occupied",
                    "560":"Att. Burglary, Forced Entry, Day, Residence",
                    "561":"Att. Burglary, Forced Entry, Day, Residence, Occupied",
                    "563":"Att. Burglary, Forced Entry, Day, Garage",
                    "565":"Att. Burglary, Forced Entry, Day, Commercial",
                    "566":"Att. Burglary, Forced Entry, Day, Commercial, Occupied",
                    "600":"Theft, Except Auto Theft",
                    "603":"Theft - Mail/Package",
                    "611":"Theft, Pocket Picking, Under $500",
                    "612":"Theft, Pocket Picking, $501 to $1000",
                    "613":"Theft, Pocket Picking, Over $1000",
                    "614":"Other",
                    "621":"Theft, Purse Snatching, Under $500",
                    "622":"Theft, Purse Snatching, $501 to $1000",
                    "623":"Theft, Purse Snatching, Over $1000",
                    "630":"Theft, Shoplifting",
                    "631":"Theft, Shoplifting, Under $500",
                    "632":"Theft, Shoplifting, $501 to $1000",
                    "633":"Theft, Shoplifting, Over $1000",
                    "640":"Theft, From Auto",
                    "641":"Theft, From Auto, Under $500",
                    "642":"Theft, From Auto, $501 to $1000",
                    "643":"Theft, From Auto, Over $1000",
                    "651":"Theft, Auto Accessories, Under $500",
                    "652":"Theft, Auto Accessories, $501 to $1000",
                    "653":"Theft, Auto Accessories, Over $1000",
                    "661":"Theft, Bicycle Theft, Under $500",
                    "662":"Theft, Bicycle Theft, $501 to $1000",
                    "663":"Theft, Bicycle Theft, Over $1000",
                    "671":"Theft, From Building, Under $500",
                    "672":"Theft, From Building, $501 to $1000",
                    "673":"Theft, From Building, Over $1000",
                    "681":"Theft, From Coin Operated Device, Under $500",
                    "682":"Theft, From Coin Operated Device, $501 to $1000",
                    "683":"Theft, From Coin Operated Device, Over $1000",
                    "691":"Theft, All Other, Under $500",
                    "692":"Theft, All Other, $501 to $1000",
                    "693":"Theft, All Other, Over $1000",
                    "700":"Motor Vehicle Theft",
                    "710":"Motor Vehicle Theft, Automobile",
                    "711":"Motor Vehicle Theft, Trucks and Buses",
                    "712":"Motor Vehicle Theft, All Other Vehicles",
                    "720":"Att. Motor Vehicle Theft, Automobile",
                    "721":"Att. Motor Vehicle Theft, Trucks and Buses",
                    "722":"Att. Motor Vehicle Theft, All Other Vehicles",
                    "730":"AUTO THEFT-OOC,STOLEN RECOVERED,AUTOMOBILES",
                    "731":"AUTO THEFT-OOC,STOLEN RECOVERED,TRUCKS & BUSES",
                    "732":"AUTO THEFT-OOC,STOLEN RECOVERED,ALL OTHER VEHICLES",
                    "810":"Asasult, Domestic",
                    "861":"Assault, Domestic, Opposite Sex",
                    "862":"Assault, Domestic, Family/Child",
                    "863":"Assault, Domestic, Gross Misdemeanor",
                    "900":"Arson",
                    "901":"Arson, Residential, Single Occupancy, Endangering Life",
                    "903":"Arson, Residential, Single Occupancy, Other",
                    "905":"Arson, Residential, Single, Abandoned, Other",
                    "911":"Arson, Residential, Multiple Occupancy, Endangering Life",
                    "913":"Arson, Residential, Multiple Occupancy, Other",
                    "915":"Arson, Residential, Multiple, Abandoned, Other",
                    "921":"Arson, Commercial, Indust/Manu, Endangering Life",
                    "922":"Arson, Commercial, Indust/Manu, Defraud Insurer",
                    "923":"Arson, Commercial, Indust/Manu, Other",
                    "925":"Arson, Commercial, Indust/Manu, Other",
                    "931":"Arson, Other Commercial, Endangering Life",
                    "933":"Arson, Other Commercial, Other",
                    "941":"Arson, Community Building, Endangering Life",
                    "942":"Arson, Community Building, Other",
                    "951":"Arson, Storage Building",
                    "961":"Arson, All Other Structures",
                    "971":"Arson, Motor Vehicle",
                    "972":"Arson, Motor Vehicle, Abandoned",
                    "975":"Arson, Other Mobile Property",
                    "981":"Arson, Not Structure",
                    "982":"Arson, Not Structure, Abandoned",
                    "1400":"Criminal Damage to Property",
                    "1401":"Graffiti",
                    "1410":"Criminal Damage to Property (Misdemeanor, Under $250)",
                    "1415":"Graffiti (Misdemeanor, Under $250)",
                    "1416":"Graffiti-Gang (Misdemeanor, Under $250)",
                    "1420":"Criminal Damage to Property (Gross Mis., $250-$500)",
                    "1425":"Graffiti (Gross Mis., $250-$500)",
                    "1426":"Graffiti-Gang (Gross Mis., $250-$500)",
                    "1430":"Criminal Damage to Property (Felony, Over $500)",
                    "1435":"Graffiti (Felony, Over $500)",
                    "1436":"Graffiti-Gang (Felony, Over $500)",
                    "1800":"Narcotics",
                    "1810":"Narcotics, Possession of Opium or Cocaine",
                    "1811":"Narcotics, Possession of Cocaine",
                    "1812":"Narcotics, Possession of Heroin",
                    "1813":"Narcotics, Possession of Methamphetamine",
                    "1814":"Narcotics, Possession of MDMA (Ecstasy)",
                    "1815":"Narcotics, Possession With Intent to Sell Cocaine",
                    "1820":"Narcotics, Possession of Synthetic Narcotic, Demerol, Etc.",
                    "1822":"Narcotics, Possession With Intent to Sell Heroin",
                    "1823":"Narcotics, Possession With Intent to Sell Methamphetamine",
                    "1824":"Narcotics, Possession With Intent to Sell MDMA (Ecstasy)",
                    "1825":"Narcotics, Possession With Intent to Sell Synthetics",
                    "1830":"Narcotics, Possession of Dangerous Non-Narcotic Drugs",
                    "1835":"Narcotics, Possession of Marijuana",
                    "1840":"Narcotics, Selling Opium, Cocaine, Etc.",
                    "1841":"Narcotics, Selling Cocaine",
                    "1842":"Narcotics, Selling Heroin",
                    "1843":"Narcotics, Selling Methamphetamine",
                    "1844":"Narcotics, Selling MDMA (Ecstasy)",
                    "1845":"Narcotics, Possession With Intent to Sell Non-Narcotics",
                    "1850":"Narcotics, Selling Synthetic Narcotics",
                    "1855":"Narcotics, Possession With Intent to Sell Marijuana",
                    "1860":"Narcotics, Selling Dangerous Non-Narcotics",
                    "1865":"Narcotics, Selling Marijuana",
                    "1870":"Narcotics, Possession of Inhalants",
                    "1880":"Narcotics, Possession of Narcotic Paraphernalia",
                    "1885":"Narcotics, Loitering With Intent to Sell Narcotics",
                    "2619":"Weapons, Discharging a Firearm in the City Limits",
                    "3100":"DEATH-INVESTIGATION OF A DEATH",
                    "9954":"Proactive Police Visit",
                    "9959":"Community Engagement Event",
                    "9986":"Proactive Foot Patrol"
            }
                
            }
        },
        methods: {
            getDate() {
                let date = new Date();
                return date.getFullYear() + "-" + date.getMonth() + "-" + date.getDay();
            },
            incrementCaseNumber() {
                this.nextCaseNumber++;
            },
            validateRequest() {
                if(this.data.code == undefined || this.data.date == undefined || this.data.grid == undefined || this.data.neighborhood == undefined || this.data.block == undefined) {
                    console.log('code: ' + this.data.code + ' date: ' + this.data.date + ' grid: ' + this.data.grid + ' neighborhood: ' + this.data.neighborhood + ' block: ' + this.data.block);
                    return false;
                }
                return true;
            },
            sendRequest() {
                if (this.validateRequest()) {
                    //send req
                    this.data.time = new Date().toLocaleTimeString();
                    this.data.type = this.types[this.data.code];
                    this.data.case = this.nextCaseNumber;
                    this.incrementCaseNumber();
                    console.log(this.data);
                } else {
                    console.log("ERRR");
                }
            }
        }
    }

</script>


<template>
    <div class="form">
        <form>
            <label>Code</label>
            <select id="code" name="code" v-model="data.code">
                <option value="100">HOMICIDE</option>
                <option value="110">Murder, Non Negligent Manslaughter</option>
                <option value="120">Murder, Manslaughter By Negligence</option>
                <option value="210">Rape, By Force</option>
                <option value="220">Rape, Attempt</option>
                <option value="300">Robbery</option>
                <option value="311">Robbery, Highway, Firearm</option>
                <option value="312">Robbery, Highway, Knife or Cutting Instrument</option>
                <option value="313">Robbery, Highway, Other Dangerous Weapons</option>
                <option value="314">Robbery, Highway, By Strong Arm</option>
                <option value="321">Robbery, Commercial House, Firearm</option>
                <option value="322">Robbery, Commercial House, Knife or Cutting Instrument</option>
                <option value="323">Robbery, Commercial House, Other Dangerous Weapons</option>
                <option value="324">Robbery, Commercial House, By Strong Arm</option>
                <option value="331">Robbery, Service Station, Firearm</option>
                <option value="333">Robbery, Service Station, Other Dangerous Weapons</option>
                <option value="334">Robbery, Service Station, By Strong Arm</option>
                <option value="341">Robbery, Convenience Store, Firearm</option>
                <option value="342">Robbery, Convenience Store, Knife or Cutting Instrument</option>
                <option value="343">Robbery, Convenience Store, Other Dangerous Weapons</option>
                <option value="344">Robbery, Convenience Store, By Strong Arm</option>
                <option value="351">Robbery, Residence, Firearm</option>
                <option value="352">Robbery, Residence, Knife or Cutting Instrument</option>
                <option value="353">Robbery, Residence, Other Dangerous Weapons</option>
                <option value="354">Robbery, Residence, By Strong Arm</option>
                <option value="361">Robbery, Bank, Firearm</option>
                <option value="363">Robbery, Bank, Other Dangerous Weapons</option>
                <option value="364">Robbery, Bank, By Strong Arm</option>
                <option value="371">Robbery, Misc., Firearm</option>
                <option value="372">Robbery, Misc., Knife or Cutting Instrument</option>
                <option value="373">Robbery, Misc., Other Dangerous Weapons</option>
                <option value="374">Robbery, Misc., By Strong Arm</option>
                <option value="400">Aggravated Assault</option>
                <option value="410">Aggravated Assault, Firearm</option>
                <option value="411">Aggravated Assault, Domestic</option>
                <option value="412">Aggravated Assault, Domestic</option>
                <option value="420">Aggravated Assault, Knife or Cutting Instrument</option>
                <option value="421">Aggravated Assault, Domestic</option>
                <option value="422">Aggravated Assault, Domestic</option>
                <option value="430">Aggravated Assault, Other Dangerous Weapons</option>
                <option value="431">Aggravated Assault, Domestic</option>
                <option value="432">Aggravated Assault, Domestic</option>
                <option value="440">Aggravated Assault, Fists/Feet/Hands</option>
                <option value="441">Aggravated Assault, Domestic</option>
                <option value="442">Aggravated Assault, Domestic</option>
                <option value="450">Aggravated Assault, Domestic</option>
                <option value="451">Aggravated Assault, Domestic</option>
                <option value="452">Aggravated Assault, Domestic</option>
                <option value="453">Aggravated Assault, Domestic</option>
                <option value="500">Burglary</option>
                <option value="510">Burglary, Forced Entry, Night, Residence</option>
                <option value="511">Burglary, Forced Entry, Night, Residence, Occupied</option>
                <option value="513">Burglary, Forced Entry, Night, Garage</option>
                <option value="515">Burglary, Forced Entry, Night, Commercial</option>
                <option value="516">Burglary, Forced Entry, Night, Commercial, Occupied</option>
                <option value="520">Burglary, No Forced Entry, Night, Residence</option>
                <option value="521">Burglary, No Forced Entry, Night, Residence, Occupied</option>
                <option value="523">Burglary, No Forced Entry, Night, Garage</option>
                <option value="525">Burglary, No Forced Entry, Night, Commercial</option>
                <option value="526">Burglary, No Forced Entry, Night, Commercial, Occupied</option>
                <option value="530">Burglary, Forced Entry, Day, Residence</option>
                <option value="531">Burglary, Forced Entry, Day, Residence, Occupied</option>
                <option value="533">Burglary, Forced Entry, Day, Garage</option>
                <option value="535">Burglary, Forced Entry, Day, Commercial</option>
                <option value="536">Burglary, Forced Entry, Day, Commercial, Occupied</option>
                <option value="540">Burglary, No Forced Entry, Day, Residence</option>
                <option value="541">Burglary, No Forced Entry, Day, Residence, Occupied</option>
                <option value="543">Burglary, No Forced Entry, Day, Garage</option>
                <option value="545">Burglary, No Forced Entry, Day, Commercial</option>
                <option value="546">Burglary, No Forced Entry, Day, Commercial, Occupied</option>
                <option value="550">Att. Burglary, Forced Entry, Night, Residence</option>
                <option value="551">Att. Burglary, Forced Entry, Night, Residence, Occupied</option>
                <option value="553">Att. Burglary, Forced Entry, Night, Garage</option>
                <option value="555">Att. Burglary, Forced Entry, Night, Commercial</option>
                <option value="556">Att. Burglary, Forced Entry, Night, Commercial, Occupied</option>
                <option value="560">Att. Burglary, Forced Entry, Day, Residence</option>
                <option value="561">Att. Burglary, Forced Entry, Day, Residence, Occupied</option>
                <option value="563">Att. Burglary, Forced Entry, Day, Garage</option>
                <option value="565">Att. Burglary, Forced Entry, Day, Commercial</option>
                <option value="566">Att. Burglary, Forced Entry, Day, Commercial, Occupied</option>
                <option value="600">Theft, Except Auto Theft</option>
                <option value="603">Theft - Mail/Package</option>
                <option value="611">Theft, Pocket Picking, Under $500</option>
                <option value="612">Theft, Pocket Picking, $501 to $1000</option>
                <option value="613">Theft, Pocket Picking, Over $1000</option>
                <option value="614">Other</option>
                <option value="621">Theft, Purse Snatching, Under $500</option>
                <option value="622">Theft, Purse Snatching, $501 to $1000</option>
                <option value="623">Theft, Purse Snatching, Over $1000</option>
                <option value="630">Theft, Shoplifting</option>
                <option value="631">Theft, Shoplifting, Under $500</option>
                <option value="632">Theft, Shoplifting, $501 to $1000</option>
                <option value="633">Theft, Shoplifting, Over $1000</option>
                <option value="640">Theft, From Auto</option>
                <option value="641">Theft, From Auto, Under $500</option>
                <option value="642">Theft, From Auto, $501 to $1000</option>
                <option value="643">Theft, From Auto, Over $1000</option>
                <option value="651">Theft, Auto Accessories, Under $500</option>
                <option value="652">Theft, Auto Accessories, $501 to $1000</option>
                <option value="653">Theft, Auto Accessories, Over $1000</option>
                <option value="661">Theft, Bicycle Theft, Under $500</option>
                <option value="662">Theft, Bicycle Theft, $501 to $1000</option>
                <option value="663">Theft, Bicycle Theft, Over $1000</option>
                <option value="671">Theft, From Building, Under $500</option>
                <option value="672">Theft, From Building, $501 to $1000</option>
                <option value="673">Theft, From Building, Over $1000</option>
                <option value="681">Theft, From Coin Operated Device, Under $500</option>
                <option value="682">Theft, From Coin Operated Device, $501 to $1000</option>
                <option value="683">Theft, From Coin Operated Device, Over $1000</option>
                <option value="691">Theft, All Other, Under $500</option>
                <option value="692">Theft, All Other, $501 to $1000</option>
                <option value="693">Theft, All Other, Over $1000</option>
                <option value="700">Motor Vehicle Theft</option>
                <option value="710">Motor Vehicle Theft, Automobile</option>
                <option value="711">Motor Vehicle Theft, Trucks and Buses</option>
                <option value="712">Motor Vehicle Theft, All Other Vehicles</option>
                <option value="720">Att. Motor Vehicle Theft, Automobile</option>
                <option value="721">Att. Motor Vehicle Theft, Trucks and Buses</option>
                <option value="722">Att. Motor Vehicle Theft, All Other Vehicles</option>
                <option value="730">AUTO THEFT-OOC,STOLEN RECOVERED,AUTOMOBILES</option>
                <option value="731">AUTO THEFT-OOC,STOLEN RECOVERED,TRUCKS & BUSES</option>
                <option value="732">AUTO THEFT-OOC,STOLEN RECOVERED,ALL OTHER VEHICLES</option>
                <option value="810">Asasult, Domestic</option>
                <option value="861">Assault, Domestic, Opposite Sex</option>
                <option value="862">Assault, Domestic, Family/Child</option>
                <option value="863">Assault, Domestic, Gross Misdemeanor</option>
                <option value="900">Arson</option>
                <option value="901">Arson, Residential, Single Occupancy, Endangering Life</option>
                <option value="903">Arson, Residential, Single Occupancy, Other</option>
                <option value="905">Arson, Residential, Single, Abandoned, Other</option>
                <option value="911">Arson, Residential, Multiple Occupancy, Endangering Life</option>
                <option value="913">Arson, Residential, Multiple Occupancy, Other</option>
                <option value="915">Arson, Residential, Multiple, Abandoned, Other</option>
                <option value="921">Arson, Commercial, Indust/Manu, Endangering Life</option>
                <option value="922">Arson, Commercial, Indust/Manu, Defraud Insurer</option>
                <option value="923">Arson, Commercial, Indust/Manu, Other</option>
                <option value="925">Arson, Commercial, Indust/Manu, Other</option>
                <option value="931">Arson, Other Commercial, Endangering Life</option>
                <option value="933">Arson, Other Commercial, Other</option>
                <option value="941">Arson, Community Building, Endangering Life</option>
                <option value="942">Arson, Community Building, Other</option>
                <option value="951">Arson, Storage Building</option>
                <option value="961">Arson, All Other Structures</option>
                <option value="971">Arson, Motor Vehicle</option>
                <option value="972">Arson, Motor Vehicle, Abandoned</option>
                <option value="975">Arson, Other Mobile Property</option>
                <option value="981">Arson, Not Structure</option>
                <option value="982">Arson, Not Structure, Abandoned</option>
                <option value="1400">Criminal Damage to Property</option>
                <option value="1401">Graffiti</option>
                <option value="1410">Criminal Damage to Property (Misdemeanor, Under $250)</option>
                <option value="1415">Graffiti (Misdemeanor, Under $250)</option>
                <option value="1416">Graffiti-Gang (Misdemeanor, Under $250)</option>
                <option value="1420">Criminal Damage to Property (Gross Mis., $250-$500)</option>
                <option value="1425">Graffiti (Gross Mis., $250-$500)</option>
                <option value="1426">Graffiti-Gang (Gross Mis., $250-$500)</option>
                <option value="1430">Criminal Damage to Property (Felony, Over $500)</option>
                <option value="1435">Graffiti (Felony, Over $500)</option>
                <option value="1436">Graffiti-Gang (Felony, Over $500)</option>
                <option value="1800">Narcotics</option>
                <option value="1810">Narcotics, Possession of Opium or Cocaine</option>
                <option value="1811">Narcotics, Possession of Cocaine</option>
                <option value="1812">Narcotics, Possession of Heroin</option>
                <option value="1813">Narcotics, Possession of Methamphetamine</option>
                <option value="1814">Narcotics, Possession of MDMA (Ecstasy)</option>
                <option value="1815">Narcotics, Possession With Intent to Sell Cocaine</option>
                <option value="1820">Narcotics, Possession of Synthetic Narcotic, Demerol, Etc.</option>
                <option value="1822">Narcotics, Possession With Intent to Sell Heroin</option>
                <option value="1823">Narcotics, Possession With Intent to Sell Methamphetamine</option>
                <option value="1824">Narcotics, Possession With Intent to Sell MDMA (Ecstasy)</option>
                <option value="1825">Narcotics, Possession With Intent to Sell Synthetics</option>
                <option value="1830">Narcotics, Possession of Dangerous Non-Narcotic Drugs</option>
                <option value="1835">Narcotics, Possession of Marijuana</option>
                <option value="1840">Narcotics, Selling Opium, Cocaine, Etc.</option>
                <option value="1841">Narcotics, Selling Cocaine</option>
                <option value="1842">Narcotics, Selling Heroin</option>
                <option value="1843">Narcotics, Selling Methamphetamine</option>
                <option value="1844">Narcotics, Selling MDMA (Ecstasy)</option>
                <option value="1845">Narcotics, Possession With Intent to Sell Non-Narcotics</option>
                <option value="1850">Narcotics, Selling Synthetic Narcotics</option>
                <option value="1855">Narcotics, Possession With Intent to Sell Marijuana</option>
                <option value="1860">Narcotics, Selling Dangerous Non-Narcotics</option>
                <option value="1865">Narcotics, Selling Marijuana</option>
                <option value="1870">Narcotics, Possession of Inhalants</option>
                <option value="1880">Narcotics, Possession of Narcotic Paraphernalia</option>
                <option value="1885">Narcotics, Loitering With Intent to Sell Narcotics</option>
                <option value="2619">Weapons, Discharging a Firearm in the City Limits</option>
                <option value="3100">DEATH-INVESTIGATION OF A DEATH</option>
                <option value="9954">Proactive Police Visit</option>
                <option value="9959">Community Engagement Event</option>
                <option value="9986">Proactive Foot Patrol</option>
            </select>
            <label>Date</label>
            <input type="date" id="date" v-model="data.date">
            <label>Police Grid</label>
            <input type="text" id="grid" v-model="data.grid" placeholder="Enter Police Grid">
            <label>Neighborhood</label>
            <input type="text" id="neighborhood" v-model="data.neighborhood" placeholder="Enter Neighborhood Number">
            <label>Address</label>
            <input type="text" id="block" v-model="data.block" placeholder="Enter Address">
            <button type="button" class="button" @click="sendRequest">Submit</button>
        </form>
    </div>
</template>

<style>
    .form {
        margin: 3rem;
    }
</style>