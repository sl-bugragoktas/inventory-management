<template>
  <div class="filter-bar">
    <div class="filter-section-label">Filters</div>

    <select v-model="selectedPeriod" class="filter-select">
      <option value="all">{{ t('filters.allMonths') }}</option>
      <option value="2025-01">{{ t('months.january') }}</option>
      <option value="2025-02">{{ t('months.february') }}</option>
      <option value="2025-03">{{ t('months.march') }}</option>
      <option value="2025-04">{{ t('months.april') }}</option>
      <option value="2025-05">{{ t('months.may') }}</option>
      <option value="2025-06">{{ t('months.june') }}</option>
      <option value="2025-07">{{ t('months.july') }}</option>
      <option value="2025-08">{{ t('months.august') }}</option>
      <option value="2025-09">{{ t('months.september') }}</option>
      <option value="2025-10">{{ t('months.october') }}</option>
      <option value="2025-11">{{ t('months.november') }}</option>
      <option value="2025-12">{{ t('months.december') }}</option>
    </select>

    <select v-model="selectedLocation" class="filter-select">
      <option value="all">{{ t('filters.all') }}</option>
      <option value="San Francisco">{{ t('warehouses.sanFrancisco') }}</option>
      <option value="London">{{ t('warehouses.london') }}</option>
      <option value="Tokyo">{{ t('warehouses.tokyo') }}</option>
    </select>

    <select v-model="selectedCategory" class="filter-select">
      <option value="all">{{ t('filters.all') }}</option>
      <option value="circuit boards">{{ t('categories.circuitBoards') }}</option>
      <option value="sensors">{{ t('categories.sensors') }}</option>
      <option value="actuators">{{ t('categories.actuators') }}</option>
      <option value="controllers">{{ t('categories.controllers') }}</option>
      <option value="power supplies">{{ t('categories.powerSupplies') }}</option>
    </select>

    <select v-model="selectedStatus" class="filter-select">
      <option value="all">{{ t('filters.all') }}</option>
      <option value="delivered">{{ t('status.delivered') }}</option>
      <option value="shipped">{{ t('status.shipped') }}</option>
      <option value="processing">{{ t('status.processing') }}</option>
      <option value="backordered">{{ t('status.backordered') }}</option>
    </select>

    <button
      class="reset-btn"
      @click="resetFilters"
      :disabled="!hasActiveFilters"
      title="Reset all filters"
    >
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" style="width:12px;height:12px;display:inline;vertical-align:middle;margin-right:4px;">
        <path fill-rule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clip-rule="evenodd" />
      </svg>
      Reset
    </button>
  </div>
</template>

<script>
import { useFilters } from '../composables/useFilters'
import { useI18n } from '../composables/useI18n'

export default {
  name: 'FilterBar',
  setup() {
    const {
      selectedPeriod,
      selectedLocation,
      selectedCategory,
      selectedStatus,
      hasActiveFilters,
      resetFilters
    } = useFilters()

    const { t } = useI18n()

    return {
      t,
      selectedPeriod,
      selectedLocation,
      selectedCategory,
      selectedStatus,
      hasActiveFilters,
      resetFilters
    }
  }
}
</script>

<style scoped>
.filter-bar {
  display: flex;
  flex-direction: column;
  gap: 6px;
  padding: 10px 8px 14px;
}

.filter-section-label {
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #475569;
  padding: 4px 6px 2px;
}

.filter-select {
  width: 100%;
  padding: 7px 28px 7px 10px;
  border-radius: 6px;
  border: 1px solid rgba(255,255,255,0.08);
  background: rgba(255,255,255,0.05);
  color: #cbd5e1;
  font-size: 0.8rem;
  font-family: inherit;
  cursor: pointer;
  appearance: none;
  -webkit-appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%2364748b' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 8px center;
  transition: border-color 0.15s;
}

.filter-select:focus {
  outline: none;
  border-color: #3b82f6;
}

.filter-select option {
  background: #1e293b;
  color: #e2e8f0;
}

.reset-btn {
  width: 100%;
  margin-top: 4px;
  padding: 7px 10px;
  border-radius: 6px;
  border: 1px solid rgba(255,255,255,0.08);
  background: transparent;
  color: #64748b;
  font-size: 0.8rem;
  font-family: inherit;
  cursor: pointer;
  transition: background 0.15s, color 0.15s, border-color 0.15s;
}

.reset-btn:not(:disabled):hover {
  background: rgba(239, 68, 68, 0.1);
  color: #f87171;
  border-color: rgba(239, 68, 68, 0.3);
}

.reset-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}
</style>
