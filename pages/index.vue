<script setup>
    import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs"

    const loading = ref(false)
    const list = [
        {
            title: "Today",
            component: resolveComponent("TabsToday")
        },
        {
            title: "Week",
            component: resolveComponent("TabsWeek")
        },
        {
            title: "Month",
            component: resolveComponent("TabsMonth")
        },
        {
            title: "Year",
            component: resolveComponent("TabsYear")
        },
    ]
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
            <Tabs defaultValue="Today" className="w-400px]">
                <TabsList>
                    <TabsTrigger v-for="(item, idx) in list" :key="idx" :value="item.title">
                        {{ item.title }}
                    </TabsTrigger>                    
                </TabsList>
                <TabsContent v-for="(item, idx) in list" :key="idx" :value="item.title">
                    <component :is="item.component"/>
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