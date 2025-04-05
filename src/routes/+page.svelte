<script lang="ts">
    import type { Dia } from "../models/dia";
    import html2canvaspro from 'html2canvas-pro';

    let grade: Dia[] = $state([])

    let qtdHorarios = 3
    let qtdDias = 5

    montaGrade()

    function montaGrade() {
        for (let i=0; i<qtdDias; i++)
            grade.push({'horarios':[]})
        
        for (var dia of grade)
            for (let i=0; i<qtdHorarios; i++)
                dia.horarios.push({'cor':0, 'local':'', 'materia':''})
    }
    
    function baixaImagem() {

        
        let grade: HTMLElement | null = document.getElementById('grade')

        html2canvaspro(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.download = 'grade gerada por horarios.png'

            el.click()
        });
    }

    function visualizaImagem() {

        
        let grade: HTMLElement | null = document.getElementById('grade')

        html2canvaspro(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.target = "_blank"

            el.click()
        });
    }

</script>

<h1 class="text-3xl">visuaulas</h1>

<p>
    Guarde seus horários bem bonitinhos com você.
</p>

<button class="bg-ctp-mauve hover:bg-[#a887d1] text-ctp-base px-3 py-2 rounded cursor-pointer transition font-semibold" onclick={()=>{baixaImagem()}}>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="inline lucide lucide-download-icon lucide-download"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" x2="12" y1="15" y2="3"/></svg>
    Baixar
</button>
<button class="bg-ctp-mauve hover:bg-[#a887d1] text-ctp-base px-3 py-2 rounded cursor-pointer transition font-semibold" onclick={()=>{visualizaImagem()}}>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="inline lucide lucide-images-icon lucide-images"><path d="M18 22H4a2 2 0 0 1-2-2V6"/><path d="m22 13-1.296-1.296a2.41 2.41 0 0 0-3.408 0L11 18"/><circle cx="12" cy="8" r="2"/><rect width="16" height="16" x="6" y="2" rx="2"/></svg>
    Ver
</button>


<div id="grade" class="flex mt-10 w-max bg-ctp-base">
    {#each grade as dia}
    <div class="mr-1">

        dia
        
            
            {#each dia.horarios as horario}
                <div class="bg-ctp-mantle w-28 h-20 mt-1 rounded-md p-3">
                    <input class="w-full font-medium" type="text" bind:value={horario.materia} name="" id="">
                    <input class="w-full text-ctp-subtext1" type="text" bind:value={horario.local} name="" id="">
                </div>
            {/each}
        
    </div>
    {/each}
</div>

