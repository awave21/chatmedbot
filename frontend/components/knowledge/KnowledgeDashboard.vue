<template>
  <div class="w-full space-y-8">
    <!-- ── Тип 1: Операционные данные (из МИС) ── -->
    <section>
      <div class="mb-2.5 flex flex-wrap items-center gap-x-3 gap-y-2">
        <span class="h-2.5 w-2.5 shrink-0 rounded-full bg-amber-500" />
        <h3 class="text-sm font-bold text-slate-900">Операционные данные</h3>
        <span
          class="inline-flex items-center gap-1.5 rounded-full bg-amber-50 px-2.5 py-1 text-[11px] font-semibold text-amber-700"
        >
          <Lock class="h-3 w-3" />
          из МИС · только чтение
        </span>
      </div>
      <p class="mb-4 max-w-3xl text-xs leading-relaxed text-slate-500 sm:text-sm">
        Точные факты клиники — цены, врачи, свободное время. Агент берёт их отсюда и никогда не выдумывает.
        Приходят из вашей CRM, здесь не редактируются.
      </p>
      <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 sm:gap-5">
        <!-- SQNS -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          :class="isSqnsEnabled ? '' : 'opacity-60'"
          @click="$emit('select', 'sqns')"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-amber-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              SQNS
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-amber-50 transition-colors group-hover:bg-amber-100 sm:h-10 sm:w-10"
              >
                <Database class="h-4 w-4 text-amber-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ sqnsTools.length }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ isSqnsEnabled ? 'подключено' : 'не подключено' }}
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Услуги, цены, специалисты, расписание и записи — синхронизируются из МИС.
          </p>
        </button>
      </div>
    </section>

    <!-- ── Тип 2: Справочные знания (заполняете вручную) ── -->
    <section>
      <div class="mb-2.5 flex flex-wrap items-center gap-x-3 gap-y-2">
        <span class="h-2.5 w-2.5 shrink-0 rounded-full bg-emerald-500" />
        <h3 class="text-sm font-bold text-slate-900">Справочные знания</h3>
        <span
          class="inline-flex items-center gap-1.5 rounded-full bg-emerald-50 px-2.5 py-1 text-[11px] font-semibold text-emerald-700"
        >
          <Pencil class="h-3 w-3" />
          заполняете вручную
        </span>
      </div>
      <p class="mb-4 max-w-3xl text-xs leading-relaxed text-slate-500 sm:text-sm">
        Регламенты, правила клиники и готовые ответы — то, что агент цитирует пациенту. Если ответа здесь
        нет, агент честно скажет, что уточнит у администратора.
      </p>
      <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 sm:gap-5">
        <!-- Прямые вопросы -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          @click="$emit('select', 'direct_questions')"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-indigo-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              Прямые вопросы
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-indigo-50 transition-colors group-hover:bg-indigo-100 sm:h-10 sm:w-10"
              >
                <MessageSquare class="h-4 w-4 text-indigo-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ directQuestions.length }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ activeDirectQuestions }} активных
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Частые вопросы с возможностью настроить фоллоуапы — автоматическую отправку сообщения через заданное время, если пользователь не ответил.
          </p>
        </button>

        <!-- Справочники -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          @click="$emit('select', 'directories')"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-emerald-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              Справочники
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-emerald-50 transition-colors group-hover:bg-emerald-100 sm:h-10 sm:w-10"
              >
                <BookOpen class="h-4 w-4 text-emerald-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ directories.length }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ totalDirectoryItems }} {{ itemsLabel(totalDirectoryItems) }}
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Частые вопросы в формате «вопрос / ответ», разбитые по категориям.
          </p>
        </button>

        <!-- Таблицы -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          @click="$emit('select', 'tables')"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-cyan-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              Таблицы
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-cyan-50 transition-colors group-hover:bg-cyan-100 sm:h-10 sm:w-10"
              >
                <Table2 class="h-4 w-4 text-cyan-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ tables.length }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ totalTableItems }} {{ itemsLabel(totalTableItems) }}
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Структурированные записи с собственными атрибутами для функций поиска, создания и обновления данных.
          </p>
        </button>

        <!-- Загрузка файлов -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          @click="$emit('select', 'file_uploads')"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-violet-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              Загрузка файлов
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-violet-50 transition-colors group-hover:bg-violet-100 sm:h-10 sm:w-10"
              >
                <FileText class="h-4 w-4 text-violet-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ uploadedFiles.length }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ indexedFiles }} проиндексировано
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Регламенты, подготовка к визиту, PDF и другие документы.
          </p>
        </button>
      </div>
    </section>

    <!-- ── Тип 3: Диалоговые сценарии (рисуете потоки) ── -->
    <section>
      <div class="mb-2.5 flex flex-wrap items-center gap-x-3 gap-y-2">
        <span class="h-2.5 w-2.5 shrink-0 rounded-full bg-purple-500" />
        <h3 class="text-sm font-bold text-slate-900">Диалоговые сценарии</h3>
        <span
          class="inline-flex items-center gap-1.5 rounded-full bg-purple-50 px-2.5 py-1 text-[11px] font-semibold text-purple-700"
        >
          <GitBranch class="h-3 w-3" />
          рисуете потоки
        </span>
      </div>
      <p class="mb-4 max-w-3xl text-xs leading-relaxed text-slate-500 sm:text-sm">
        Не факты, а манера общения: как объяснить процедуру, снять сомнение, ответить на «дорого», каким
        тоном вести к записи.
      </p>
      <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 sm:gap-5">
        <!-- Потоки эксперта (переход на отдельную страницу) -->
        <button
          type="button"
          class="group relative flex w-full cursor-pointer flex-col overflow-hidden rounded-3xl border border-slate-100 bg-white p-5 text-left shadow-[0_2px_12px_-4px_rgba(0,0,0,0.04)] transition-all duration-500 sm:p-6 hover:-translate-y-1 hover:shadow-[0_20px_40px_-12px_rgba(0,0,0,0.08)]"
          @click="goToScriptFlows"
        >
          <div
            class="pointer-events-none absolute -right-8 -top-8 h-24 w-24 rounded-full bg-purple-500/5 transition-transform duration-700 group-hover:scale-150"
          />
          <div class="relative z-10 mb-4 flex items-center justify-between">
            <p
              class="text-xs font-normal text-slate-600 transition-colors sm:text-sm group-hover:text-primary"
            >
              Потоки эксперта
            </p>
            <div class="flex items-center gap-2">
              <ChevronRight
                class="h-4 w-4 text-slate-400 opacity-0 transition-all duration-300 group-hover:translate-x-0.5 group-hover:opacity-100"
              />
              <div
                class="flex h-9 w-9 shrink-0 items-center justify-center rounded-lg bg-purple-50 transition-colors group-hover:bg-purple-100 sm:h-10 sm:w-10"
              >
                <GitBranch class="h-4 w-4 text-purple-600 sm:h-5 sm:w-5" />
              </div>
            </div>
          </div>
          <p class="relative z-10 mb-2 text-3xl font-bold text-slate-900 sm:text-4xl">
            {{ scriptFlowsCount }}
          </p>
          <p class="relative z-10 mb-3 text-xs text-slate-500 sm:text-sm">
            {{ publishedScriptFlows }} опубликовано
          </p>
          <p class="relative z-10 text-xs leading-relaxed text-slate-500 sm:text-sm">
            Тактики, работа с возражениями и тон диалога на визуальной схеме.
          </p>
        </button>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { navigateTo } from '#app'
import { BookOpen, ChevronRight, Database, FileText, GitBranch, Lock, MessageSquare, Pencil, Table2 } from 'lucide-vue-next'
import { useScriptFlows } from '~/composables/useScriptFlows'
import type { Directory } from '~/types/directories'
import type { DirectQuestion, KnowledgeFileItem } from '~/types/knowledge'
import type { SqnsTool } from '~/composables/useAgents'
import type { TableItem } from '~/types/tables'

const props = defineProps<{
  directQuestions: DirectQuestion[]
  directories: Directory[]
  tables: TableItem[]
  files: KnowledgeFileItem[]
  sqnsTools: SqnsTool[]
  isSqnsEnabled: boolean
}>()

defineEmits<{
  (e: 'select', tab: string): void
}>()

const route = useRoute()
const agentId = computed(() => (route.params.id as string) || '')
const goToScriptFlows = () => {
  if (agentId.value) navigateTo(`/agents/${agentId.value}/scripts`)
}

// Потоки эксперта живут на отдельной странице — подтягиваем их счётчик напрямую,
// чтобы плитка показывала реальное число, как остальные разделы базы знаний.
const scriptFlowsApi = agentId.value ? useScriptFlows(agentId.value) : null
const scriptFlowsCount = computed(() => scriptFlowsApi?.flows.value.length ?? 0)
const publishedScriptFlows = computed(
  () => (scriptFlowsApi?.flows.value ?? []).filter((f) => f.flow_status === 'published').length,
)
onMounted(() => {
  scriptFlowsApi?.fetchFlows().catch(() => {})
})

const activeDirectQuestions = computed(() => props.directQuestions.filter((q) => q.is_enabled).length)
const totalDirectoryItems = computed(() => props.directories.reduce((acc, d) => acc + (d.items_count ?? 0), 0))
const totalTableItems = computed(() => props.tables.reduce((acc, d) => acc + (d.records_count ?? 0), 0))
const uploadedFiles = computed(() => props.files.filter((f) => f.type === 'file'))
const indexedFiles = computed(() => uploadedFiles.value.filter((f) => f.vector_status === 'indexed').length)

const itemsLabel = (count: number) => {
  if (count % 10 === 1 && count % 100 !== 11) return 'запись'
  if (count % 10 >= 2 && count % 10 <= 4 && (count % 100 < 10 || count % 100 >= 20)) return 'записи'
  return 'записей'
}
</script>
