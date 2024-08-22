<script setup>
    import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"

    let currentCategory = ref('today'); 
    let data = ref([])   
    const list = [
        {
            title: "Today"
        },
        {
            title: "Week",            
        },
        {
            title: "Month",
        },
        {
            title: "Year",
        },
    ]        

    const setCategory = (e) => {
        let v = e.target.innerText.toLowerCase();
        currentCategory.value = v;
        switch (v) {
            case 'today':
                generatorRandomValue(24);
                break;
            case 'week':
                generatorRandomValue(7);
                break;
            case 'month':
                generatorRandomValue(31);
                break;
            case 'year':
                generatorRandomValue(12);
                break;
            default:
                generatorRandomValue(24);
        }
    }

    function generatorRandomValue(number = 7) {
        let values = [];
        for (let i = 0; i<number; i++) {
            values.push(Math.random() * 100);
        }
        data.value = values;
        return data;
    }

    const cards = [
        {
            title: "Sales",
            progression: 12,
            amount: 1244.44,
            label: "View sales",
            description: "Sales of March 2024",
            icon: "solar:ticket-sale-outline",
        },
        {
            title: "Refunds",
            progression: 8,
            amount: 84.44,
            label: "View refunds",
            description: "Refunds since beginning of year",
            icon: "heroicons-outline:reciept-refund",
        },
        {
            title: "Payout",
            progression: 14,
            amount: 899.44,
            label: "View payout",
            description: "Payout of this week",
            icon: "tabler:zoom-money",
        },
    ]

    onMounted(() => {
        generatorRandomValue(24);
    })

    
</script>

<template>
    <div class="grid w-full gap-4">
        <header class="flex items-start justify-between">
            <div class="grow">
                <p>Hi, Welcome back Rahmat !</p>
                <h1>Dashboard</h1>
            </div>
            <div class="w-[120px] h-[36px] bg-neutral-200"></div>
        </header>
        <main class="grid gap-4">
            <!-- <div class="flex items-center gap-4">
                <div v-for="(item, idx) in 3" :key="idx" class="w-[120px] h-[36px] bg-neutral-200"></div>
            </div>            
            <section>
                <div class="w-full h-[360px] bg-neutral-200"></div>
            </section> -->
            <Tabs defaultValue="Today">
                <TabsList  className="max-w-[400px]">
                    <TabsTrigger v-for="(item, idx) in list" :key="idx" :value="item.title" @click="setCategory">
                        {{ item.title }}
                    </TabsTrigger>                    
                </TabsList>
                <TabsContent v-for="(item, idx) in list" :key="idx" :value="item.title">
                    <Chart v-if="data.length" :currentCategory="currentCategory" :data="data"/>
                </TabsContent>                
            </Tabs>
        </main>
        <footer>
           <div class="flex items-center gap-4">
                <div v-for="(item, idx) in 3" :key="idx" class="w-full h-[260px] bg-neutral-200"></div>
           </div>
        </footer>
    </div>
</template>