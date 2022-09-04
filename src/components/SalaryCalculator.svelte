<script lang="ts">
	import { t, locale, locales } from '../locale/i18n';
	import SalaryCalculatorGroupCard from './SalaryCalculatorGroupCard.svelte';
	import SalaryCalculatorNumberInput from './SalaryCalculatorNumberInput.svelte';

	export let title: string | undefined = undefined;
	export let description: string | undefined = undefined;
	export let year: number = 2022;
	const years: number[] = [2022, 2021];
	export let salary: number = 450000;

	let pensionSavingsEmployeeContributionPercentage: number = 4.0;
	let pensionSavingsEmployerContributionAmount: number = 0;
	let pensionSavingsEmployerContributionPercentage: number = 11.5;
	let rehabilitationFundPercentage: number = 0.1;
	let additionalPensionSavingsEmployeeContributionPercentage: number = 2;
	let additionalPensionSavingsEmployerContributionPercentage: number = 2;

	let incomeTaxStep1Percentage: number = 31.45;
	let incomeTaxStep2Percentage: number = 37.95;
	let incomeTaxStep3Percentage: number = 46.25;
	let incomeTaxStep1Max: number = 349018;
	let incomeTaxStep2Max: number = 979847;

	let insuranceFeePercentage: number = 6.35;

	let personalTaxAllowance: number = 53916;
	let personalTaxAllowanceUsedPercentage: number = 100;

	let unionFeePercentage: number = 0.0;
	let unionFee: number = 0.0;

	let privateSectorReliefFundPercentage: number = 0.0;
	let vacationFundPercentage: number = 0.0;
	let educationFundPercentage: number = 0.0;

	$: totalEmployeeContribution = 0;
	$: totalEmployerContribution = 0;
	$: totalCost = 0;
	$: paidSalary = 0;
</script>

<div class="flex flex-col items-center justify-center space-y-4 border rounded p-4 shadow-2xl">
	<select bind:value={$locale}>
		{#each locales as l}
			<option value={l}>{l}</option>
		{/each}
	</select>
	<h1 class="text-3xl">{title ?? $t('salary_calculator.title')}</h1>
	<h2 class="text-2xl text-gray-700 truncate">
		{description ?? $t('salary_calculator.description')}
	</h2>
	<div class="felx flex-col items-center">
		<label for="year">Year</label>
		<select bind:value={year}>
			{#each years as y}
				<option value={y}>{y}</option>
			{/each}
		</select>
	</div>
	<div class="flex flex-row float-none">
		<div>
			<label for="salary">Salary</label>
			<input type="number" bind:value={salary} class="border border-black pl-1 " />
		</div>
		<div>
			<label for="personalTaxAllowanceUsedPercentage">Personal Tax Allowance Used (%)</label>
			<input
				type="number"
				bind:value={personalTaxAllowanceUsedPercentage}
				class="border border-black pl-1 "
			/>
		</div>
	</div>
	<div class="flex flex-row flex-none space-x-4">
		<SalaryCalculatorGroupCard
			title="Pension Fund"
			description="The minimum mandatory contribution to a pension fund is 12% of total wages from age 16 to 70.

		Wage agreements cover payments into pension funds. The general rule is that the wage earner pays 4% of his/her total wages, and the matching contribution of the wage payer is 11.5%, total contribution of 15.5%. This applies equally to state and municipal civil servants.
		
		The foregoing describes the general rule, but there are exceptions to it, such as for bank employees and employees in older state and municipal pension systems."
		>
			<SalaryCalculatorNumberInput
				label="Workers premium"
				value={salary}
				percentage={pensionSavingsEmployeeContributionPercentage}
				on:total={(e) => (pensionSavingsEmployerContributionAmount = e.detail.total)}
			/>
			<SalaryCalculatorNumberInput
				label="Employer contribution"
				value={salary}
				percentage={pensionSavingsEmployerContributionPercentage}
				on:total={(e) => (pensionSavingsEmployerContributionAmount = e.detail.total)}
			/>
			<SalaryCalculatorNumberInput
				label="Rehabilitation fund"
				value={salary}
				percentage={pensionSavingsEmployeeContributionPercentage}
				on:total={(e) => (pensionSavingsEmployerContributionAmount = e.detail.total)}
			/>
			<div />
			<p>Additional Pension Savings</p>
			<SalaryCalculatorNumberInput
				label="Employee contribution"
				value={salary}
				percentage={pensionSavingsEmployeeContributionPercentage}
				on:total={(e) => (pensionSavingsEmployerContributionAmount = e.detail.total)}
			/>
			<SalaryCalculatorNumberInput
				label="Employer contribution"
				value={salary}
				percentage={pensionSavingsEmployeeContributionPercentage}
				on:total={(e) => (pensionSavingsEmployerContributionAmount = e.detail.total)}
			/>
		</SalaryCalculatorGroupCard>
		<SalaryCalculatorGroupCard title="Income tax" description="" />
		<SalaryCalculatorGroupCard title="Unions and funds" description="" />
	</div>

	<h2>Summary</h2>
	<div class="flex flex-row items-center">
		<p class="mx-5">Sallary: {salary ? 0 : salary} kr.</p>
		<p class="mx-5">Workers premium : {pensionSavingsEmployerContributionAmount} kr.</p>
		<p class="mx-5">Employee contribution: {totalEmployeeContribution} kr.</p>
		<p class="mx-5">Employer contribution: {totalEmployerContribution} kr.</p>
		<p class="mx-5">Total cost: {totalCost} kr.</p>
		<p class="mx-5">Paid salary: {paidSalary} kr.</p>
	</div>
</div>
