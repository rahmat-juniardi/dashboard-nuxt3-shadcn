<script setup>
let props = defineProps(["currentCategory", "data"]);
let data = props.data || [];
let currentCategory = props.currentCategory || "today";

let categories = ref({
    'today': ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00', '06:00', '07:00', '08:00', '09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00', '20:00', '21:00', '22:00', '23:00'],
    'week': ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
    'year': ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
});
    
const chartOptions = computed(() => (
    {
        chart: {
            type: 'line',
            animation: {
                enabled: false
            }
        },
        legend: {
            enabled: false,
        },
        credits: {
            enabled: false,
        },
        title: {
            text: ''
        },
        xAxis: {
            gridLineColor: 'transparent',
            categories: categories.value[currentCategory],
        },
        yAxis: {
            gridLineColor: 'transparent',
            title: {
                text: ''
            }
        },
        plotOptions: {
            line: {
                marker: {
                    enabled: false
                },
                dataLabels: {
                    enabled: false
                },
                enableMouseTracking: true
            }
        },
        series: [{
            name: 'line',
            lineWidth: '4px',
            color: {
                linearGradient: {},
                stops: [
                    [0, 'orange'],
                    [0.33, 'red'],
                    [0.66, 'purple'],
                    [1, 'green']
                ]
            },
            data: data
        }]
    }
))

function generateMonth() {
    let currentDate = new Date();
    let currentMonth = currentDate.getMonth() + 1;
    let currentYear = currentDate.getFullYear();

    function generateMonthDates() {
        let monthDates = [];
        let daysInMonth = new Date(currentYear, currentMonth, 0).getDate();

        for (let i = 1; i <= daysInMonth; i++) {
            let dayString = ("0" + i).slice(-2);
            let monthString = ("0" + currentMonth).slice(-2);
            monthDates.push(monthString + "/" + dayString);
        }

        return monthDates;
    }

    let month = generateMonthDates();
    categories.value = ({...categories.value, month})
    return month;
}

onMounted(() => {    
    generateMonth();
})

</script>

<template>
    <div class="border p-4 rounded-lg"> 
        <highchart :options="chartOptions" />    
    </div>
</template>