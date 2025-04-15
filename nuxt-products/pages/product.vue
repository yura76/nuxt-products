<script setup lang="ts">
import type { TableColumn } from '@nuxt/ui'
import { getPaginationRowModel } from '@tanstack/vue-table'


const table = useTemplateRef('table')
const UButton = resolveComponent('UButton')


type Product = {
  id: number
  title: string
  description: string
  price: number
  rating: number
  brand: string
  category: string
  thumbnail: string
}

const { data: products, status, error } = await useFetch<Product[]>('https://dummyjson.com/products', {
  transform: (response: any) => response.products,
  server: false
})

useHead({ title: 'Список продуктів' })


const columns: TableColumn<Product>[] = [
  {
    accessorKey: 'title',
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Назва',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    },
  },
  {
    accessorKey: 'description',
    size: 120,
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Опис',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5 ',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    },
    cell: ({ row }) =>
        h('p', {
          class: 'min-w-[100px]',
        }, row.original.description)
  },
  {
    accessorKey: 'price',
    cell: ({ row }) => `${row.original.price}`,
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Ціна',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    }

  },
  {
    accessorKey: 'rating',
    cell: ({ row }) =>
        h('p', {
          class: `font-bold ${row.original.rating < 4.5 ? 'text-red-500' : 'text-green-600'}`
        }, row.original.rating.toFixed(1)),
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Оцінка',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    }

  },
  {
    accessorKey: 'brand',
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Бренд',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    }

  },
  {
    accessorKey: 'category',
    enableSorting: true,
    header: ({ column }) => {
      const isSorted = column.getIsSorted()

      return h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        label: 'Категорія',
        icon: isSorted
            ? isSorted === 'asc'
                ? 'i-lucide-arrow-up-narrow-wide'
                : 'i-lucide-arrow-down-wide-narrow'
            : 'i-lucide-arrow-up-down',
        class: '-mx-2.5',
        onClick: () => {
          const currentSort = column.getIsSorted()
          if (!currentSort) {
            column.toggleSorting(false) //   за зростанням
          } else if (currentSort === 'asc') {
            column.toggleSorting(true) //  за спаданням
          } else {
            column.clearSorting() // скинути сортування
          }
        }
      })
    }

  },
  {
    accessorKey: 'thumbnail',
    header: 'Фото',
    cell: ({ row }) =>
        h('img', {
          src: row.original.thumbnail,
          class: 'min-w-[100px] min-h-[100px]',
          alt: 'thumbnail'
        })
  },
]


const globalFilter = ref('')

const pagination = ref({
  pageIndex: 0,
  pageSize: 10
})

</script>

<template>
  <div class="p-8 max-w-7xl mx-auto">
    <div v-if="status ==='pending'" class="text-center py-4">
      <UProgress animation="carousel" />
      <div class="mt-2">Завантаження даних...</div>
    </div>

    <div v-else-if="error">
      <UAlert
          title="Помилка завантаження"
          :description="error.message"
          icon="i-heroicons-exclamation-triangle"
          variant="solid"
      />
    </div>

    <div v-else>
      <div class="mb-4 flex justify-between items-center">
        <UInput
            v-model="globalFilter"
            class="max-w-sm"
            placeholder="Filter..."
        />

        <UPagination
            :default-page="(table?.tableApi?.getState().pagination.pageIndex || 0) + 1"
            :items-per-page="table?.tableApi?.getState().pagination.pageSize"
            :total="table?.tableApi?.getFilteredRowModel().rows.length"
            @update:page="(p) => table?.tableApi?.setPageIndex(p - 1)"
        />
      </div>

      <UTable
          ref="table"
          :data="products ?? []"
          :columns="columns"
          :pagination-options="{
              getPaginationRowModel: getPaginationRowModel()
             }"
          v-model:pagination="pagination"
          v-model:global-filter="globalFilter"
      >
      </UTable>

    </div>
  </div>
</template>
