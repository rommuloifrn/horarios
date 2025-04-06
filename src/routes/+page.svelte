<script lang="ts">
    import html2canvaspro from 'html2canvas-pro';
    import type { Dia } from "../models/dia";
    import type { Horario } from "../models/horario";

    let grade: Dia[] = $state([])

    let qtdHorarios = 3
    let qtdDias = 5

    let diasDaSemana = [
        'Segunda',
        'Terça',
        'Quarta',
        'Quinta',
        'Sexta',
        'Sábado',
        'Domingo'
    ]

    montaGrade()

    function inverteHiddenDaMarca() {
        let marca: HTMLElement | null = document.getElementById('marca')
        marca!.hidden = !marca!.hidden
    }

    function montaGrade() {
        for (let i=0; i<qtdDias; i++)
            grade.push({'horarios':[]})
        
        for (var dia of grade)
            for (let i=0; i<qtdHorarios; i++)
                dia.horarios.push({'cor':0, 'local':'', 'materia':''})
    }
    
    function baixaImagem() {
        inverteHiddenDaMarca()
        
        let grade: HTMLElement | null = document.getElementById('quadro')

        html2canvaspro(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.download = 'grade gerada por horarios.png'

            el.click()
        });
        inverteHiddenDaMarca()
    }

    function visualizaImagem() {
        inverteHiddenDaMarca()
        
        let grade: HTMLElement | null = document.getElementById('quadro')

        html2canvaspro(grade!).then(function(canvas) {
            let link = canvas.toDataURL()
            
            let el: any = document.createElement("a")
            el.href = link;
            el.target = "_blank"

            el.click()
        });
        inverteHiddenDaMarca()
    }

    function horarioEstaPreenchido(horario: Horario) {
        return (horario.materia != "") || (horario.local != "")
    }

</script>

<h1 class="text-3xl bg-clip-text text-transparent bg-gradient-to-r from-ctp-mauve to-ctp-pink font-bold">visuaulas</h1>

<p>
    Guarde seus horários bem bonitinhos com você.
</p>

<div id="quadro" class="bg-ctp-base mt-10 p-3">
    <div id="grade" class="flex w-max">
        
        {#each grade as dia, index}
        <div class="mr-1">
    
            <span class="text-ctp-surface2">
                {diasDaSemana[index]}
            </span>
            
                
                {#each dia.horarios as horario}
                    <div class="group bg-ctp-mantle w-32 h-20 mt-1 rounded-md p-3 {horarioEstaPreenchido(horario) ? "bg-ctp-sky text-ctp-base" : ""}">
                        <div class="{horarioEstaPreenchido(horario) ? 'block' : 'hidden'} group-hover:block">
                            <input class="w-full font-medium placeholder:text-ctp-surface2" type="text" bind:value={horario.materia} name="" id="" placeholder="Matéria">
                            <input class="w-full text-sm placeholder:text-ctp-surface2" type="text" bind:value={horario.local} name="" id="" placeholder="Local">
                        </div>
                    </div>
                {/each}
            
        </div>
        {/each}
    </div>
    <div id="marca" hidden class="mt-2">
        Imagem gerada usando <span class="text-ctp-pink font-bold">visuaulas</span>
    </div>
</div>

<button class="mt-2 bg-ctp-mauve hover:bg-[#a887d1] text-ctp-base px-3 py-2 rounded cursor-pointer transition font-semibold" onclick={()=>{baixaImagem()}}>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="inline lucide lucide-download-icon lucide-download"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" x2="12" y1="15" y2="3"/></svg>
    Baixar
</button>
<button class="bg-ctp-mauve hover:bg-[#a887d1] text-ctp-base px-3 py-2 rounded cursor-pointer transition font-semibold" onclick={()=>{visualizaImagem()}}>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="inline lucide lucide-images-icon lucide-images"><path d="M18 22H4a2 2 0 0 1-2-2V6"/><path d="m22 13-1.296-1.296a2.41 2.41 0 0 0-3.408 0L11 18"/><circle cx="12" cy="8" r="2"/><rect width="16" height="16" x="6" y="2" rx="2"/></svg>
    Ver
</button>


<footer class="absolute bottom-[0] mb-6">
    by <a href="https://github.com/rommuloifrn" target="_blank" class="text-ctp-red underline italic">romulo</a> usando o tema <a target="_blank" class="text-ctp-red" href="https://catppuccin.com/">catppuccin</a>.
</footer>
