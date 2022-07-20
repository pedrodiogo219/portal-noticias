<template>
    <h1>Últimas notícias</h1>

    <!-- <input type="text" v-model="input" placeholder="buscar noticia..." /> -->
    <input
        v-model="input"
        type="text"
        name="q"
        id="search"
        placeholder="Buscar notícia..."
        aria-label="Search"/>

    <div id="listaNoticias" v-if="noticiasExists()">
        <ResumoNoticia v-for="(noticia, index) in filtraNoticias()" :key="index" :noticia="noticia"></ResumoNoticia>
    </div>
    <div v-else>
        <p>Nenhuma notícia disponivel</p>

        <button v-on:click="exemplos()">Adicionar exemplos de notícias</button>
    </div>

</template>

<script>
import router from '@/router';
import ResumoNoticia from './ResumoNoticia.vue';
import { ref } from 'vue';
    export default {
   
    input: ref(''),
    data() {
        return {
            input: ref(''),
            noticiasExists: () => {
                return (JSON.stringify(this.$parent.noticias.value) != '[]')
            }
        }
    },
    created(){
      this.input = ref('');  
    },
    methods:{
        filtraNoticias(){
            return  this.$parent.noticias.value.filter(
                        (noticia) => {
                        return noticia.titulo.toLowerCase().includes(this.input.toLowerCase())
                        }
                    );
        },
        exemplos(){
            
            const noticiasExemplo = [
                {
                    id: 1,
                    titulo: "Celsius, once a crypto highflier, files for bankruptcy",
                    descricao: `The crypto firm said most account activity is still "paused." It's unclear whether depositors will get their money back.`,
                    corpo: `Celsius Network filed for bankruptcy protection on Wednesday after a "crypto winter" — or crash — that decimated the value of digital currencies including bitcoin and ethereum. The company said most accounts will continue to be "paused until further notice." Celsius is the third crypto-related firm to file for bankruptcy protection in two weeks. It follows Three Arrows Capital and lender Voyager Digital in seeking financial restructuring after digital currencies plunged in value. Celsius marketed itself as a type of crypto bank, encouraging people to deposit their digital currencies with the firm, and then earning money by either borrowing or lending against the crypto deposits. Troubles for Celsius' customers started when the network halted trading and other activities last month amid the crypto meltdown, effectively blocking customers from accessing their funds. The decision shocked customers who had been told by Celsius that the platform was low-risk and secure, all while providing earnings as high as 17%. In its sales pitch, Celsius pledged "Your interests are our top priority" and stressed that traditional banking "is broken."`,
                    imagem: "https://blocktrends.com.br/wp-content/uploads/2022/06/uMB9fZg-780x500.jpeg"
                },
                {
                    id: 2,
                    titulo: "Twitter stock plunges on prospect of legal battle with Elon Musk",
                    descricao: "After billionaire Elon Musk said that he was abandoning his $44 billion buyout, Twitter vowed to pursue him in court.",
                    corpo: `Shares of Twitter plummeted on Monday afternoon on the prospect of a prolonged legal fight between the social media company and billionaire Elon Musk, who says he's pulling out of a buyout deal, leaving Twitter's future in doubt.
                            In announcing he was dropping the deal on Friday, Musk claimed that Twitter refused to provide enough information about the number of fake accounts it has and that Musk's advisors determined the true incidence of bots on the platform is "wildly higher" than Twitter claims. The social media platform then vowed to challenge Musk in court to uphold the agreement, and has hired powerhouse law firm Wachtell, Lipton, Rosen & Katz in preparation for filing a lawsuit this week in Delaware Court of Chancery, according to Bloomberg. 
                            Generally, acquisition agreements are exceeedingly difficult to get out of.  "Once you're into the world where you already have the agreement, it's rare for people to try to pull out," said Mathieu Shapiro, managing partner at Obermayer, who specializes in business litigation. "As a basic premise, the Delaware court will want to enforce that merger agreement, and that will be their starting place."`,
                    imagem: "https://www.cnnbrasil.com.br/wp-content/uploads/sites/12/2021/06/29316_D916368809E6CAD8-1.jpg?w=876&h=484&crop=1"
                },
                {
                    id: 3,
                    titulo: "Yelp to close 3 U.S. offices, saying the \"future of work\" is remote",
                    descricao: "Employees at the online review company used less than 2% of its office space in Chicago, New York and Washington, D.C.",
                    corpo: `Yelp is closing three of its U.S. offices after finding most of its employees prefer to work remotely.
                            In a blog post Thursday, Yelp Cofounder and CEO Jeremy Stoppelman said the company will close its offices in Chicago, New York and Washington, D.C., on July 29. The online review and reservation company also plans to downsize its office in Phoenix.
                            "Combined, the three offices we're closing saw a weekly average utilization of less than 2% of the available workspaces," Stoppelman wrote.
                            Job postings for remote work rise, as many say they like it
                            Elon Musk says remote work is "no longer acceptable"
                            Airbnb allows employees to live and work from anywhere
                            San Francisco-based Yelp announced a remote-first work model in February 2021. Stoppelman said Yelp has proven it can be successful with a remote workforce, noting that the company achieved record revenue of just over $1 billion in 2021.`,
                    imagem: "https://geekblog.com.br/wp-content/uploads/2015/03/yelp_estimate_tool.jpg"
                },
                {
                    id: 4,
                    titulo: "Cachorrinho Bonitinho",
                    descricao: "Examente aquilo que você procura",
                    corpo: "Aprecie essa bela imagem de um cachorrinho",
                    imagem: "https://s2.glbimg.com/eQkhAB2FrlFSMj_Jbkw024ueqao=/e.glbimg.com/og/ed/f/original/2019/01/19/50898568_10157219683273254_5268539131058716672_o.jpg"
                }
            ]

            localStorage.setItem("noticias", JSON.stringify(noticiasExemplo))
            router.go(); // refreshes the page

        }
    },
    components: { ResumoNoticia }
}
</script>


<style scoped>

#listaNoticias{
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
}

#search{
    min-width: 200px;
}

</style>