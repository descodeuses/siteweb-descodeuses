<script>
import BaseButton from '@/components/elements/Button.vue'

export default {
	components: {
		BaseButton
	},
	data() {
		return {
			exp: {
				experiences: {},
				language: {},
				languageLevel: {}
			}
		}
	},
	created() {
		let form = this.$store.getters['register/form']
		if (form.experiences) this.exp = form.experiences
	},
	methods: {
		goBack() {
			this.$store.dispatch('register/updateExperieces', this.exp)
			this.$emit('prevStep')
		},
		validate() {
			this.$validator.validateAll().then(result => {
				if (!result) return
				this.$store.dispatch('register/updateExperieces', this.exp)
				this.$emit('nextStep')
			})
		}
	}
}
</script>

<template>
	<div class="col s8 offset-s2">
		<h1 class="center-align">Critères de candidature</h1>
		<span class="help-text center-align">* les champs sont obligatoires</span>
		<div class="row">
			<form v-on:submit.prevent v-on:submit="validate()">
				<div class="row">
					<div class="input-field col s12">
						<h2>Avez-vous déjà eu une expérience en programmation et/ou de manipulation de données avant ? *</h2>
						<p>
							<label for="yes">
								<input
									type="radio"
									id="yes"
									v-model="exp.experiences.code"
									:value="true"
									name="experience"
									v-validate="'required'"
								/>
								<span>Oui, j'ai déjà codé</span>
							</label>
						</p>
						<p>
							<label for="no">
								<input
									type="radio"
									id="no"
									:value="false"
									v-model="exp.experiences.code"
									name="experience"
									v-validate="'required'"
								/>
								<span>Non, aucune experience</span>
							</label>
						</p>
						<span class="helper-text" data-error="Ce champs obligatoire"></span>
					</div>

					<div class="control" v-if="exp.experiences.experience">
						<h2>Racontez-nous vos expériences</h2>
						<textarea
							name="experience_code"
							id="experience_code"
							cols="30"
							rows="5"
							class="materialize-textarea"
							v-model="exp.experiences.experience_code"
							v-validate="'required'"
						></textarea>
						<span class="helper-text" data-error="Ce champs obligatoire"></span>
					</div>

					<div class="control" v-else-if="!exp.experiences.experience">
						<h2>Pourquoi vouloir intégrer cette formation ?</h2>
						<textarea
							name="hasNoExperiences"
							id="hasNoExperiences"
							cols="30"
							rows="5"
							class="materialize-textarea"
							v-model="exp.experiences.hasNoExperiences"
							v-validate="'required'"
						></textarea>
						<span class="helper-text" data-error="Ce champs obligatoire"></span>
					</div>
				</div>
				<div class="row">
					<h2>Quel est votre dernier diplôme obtenu ? *</h2>
					<p class="help-text">Information demandée à titre indicatif, en aucun cas discriminant !</p>
					<input
						name="diplome"
						type="text"
						class="input"
						placeholder="ex. bac"
						v-model="exp.experiences.diplome"
						v-validate="'required'"
					/>
					<span class="helper-text" data-error="Ce champs obligatoire"></span>
				</div>
				<div class="row">
					<h2 for>Racontez-nous en quelques phrases votre histoire. *</h2>
					<p
						class="help"
					>Tout nous intéresse : études, travail, voyages, et autres occupations et passions.</p>
					<textarea
						name="ownHistory"
						id="ownHistory"
						cols="30"
						rows="10"
						class="materialize-textarea"
						v-model="exp.experiences.ownHistory"
						v-validate="'required'"
					></textarea>
					<span class="helper-text" data-error="Ce champs obligatoire"></span>
				</div>
				<div class="row">
					<h2>Vos langues</h2>
					<p
						class="help-text"
					>Information demandée à titre indicatif, ce n'est pas éliminatoire, ni déterminant</p>
					<div class="field-body">
						<div class="col s6">
							<div class="control">
								<label for="french">
									<input
										type="checkbox"
										class
										name="language"
										v-model="exp.language.french"
										value="french"
										id="french"
									/>
									<span>Français</span>
								</label>
							</div>
							<template v-if="exp.language.french">
								<div class="control">
									<label for="advancedFrench">
										<input
											type="radio"
											id="advancedFrench"
											v-model="exp.languageLevel.french"
											value="advanced"
											name="languageLevelFrench"
										/>
										<span>Avancé</span>
									</label>
								</div>
								<div class="control">
									<label for="intermediaryFrench">
										<input
											type="radio"
											id="intermediaryFrench"
											v-model="exp.languageLevel.french"
											value="intermediary"
											name="languageLevelFrench"
										/>
										<span>Intermedière</span>
									</label>
								</div>
								<div class="control">
									<label for="beginningFrench">
										<input
											type="radio"
											id="beginningFrench"
											v-model="exp.languageLevel.french"
											value="beginning"
											name="languageLevelFrench"
										/>
										<span>Débutant.e</span>
									</label>
								</div>
							</template>
						</div>
						<div class="col s6">
							<div class="control">
								<label for="english">
									<input type="checkbox" class v-model="exp.language.english" value="english" id="english" />
									<span>Anglais</span>
								</label>
							</div>

							<template v-if="exp.language.english">
								<div class="control">
									<label for="advancedEnglish">
										<input
											type="radio"
											id="advancedEnglish"
											v-model="exp.languageLevel.english"
											value="advanced"
											name="languageLevelEnglish"
										/>
										<span>Avancé</span>
									</label>
								</div>
								<div class="control">
									<label for="intermediaryEnglish">
										<input
											type="radio"
											id="intermediaryEnglish"
											v-model="exp.languageLevel.english"
											value="intermediary"
											name="languageLevelEnglish"
										/>
										<span>Intermedière</span>
									</label>
								</div>
								<div class="control">
									<label for="beginningEnglish">
										<input
											type="radio"
											id="beginningEnglish"
											v-model="exp.languageLevel.english"
											value="beginning"
											name="languageLevelEnglish"
										/>
										<span>Débutant.e</span>
									</label>
								</div>
							</template>
						</div>
						<div class="col s6">
							<div class="control">
								<label for="arabic">
									<input
										type="checkbox"
										class
										v-model="exp.language.arabic"
										name="language"
										value="arabic"
										id="arabic"
									/>
									<span>Arabe</span>
								</label>
							</div>
							<template v-if="exp.language.arabic">
								<div class="control">
									<label for="advancedArabic">
										<input
											type="radio"
											id="advancedArabic"
											v-model="exp.languageLevel.arabic"
											name="languageLevelArabic"
											value="advanced"
										/>
										<span>Avancé</span>
									</label>
								</div>
								<div class="control">
									<label for="intermediaryArabic">
										<input
											type="radio"
											id="intermediaryArabic"
											v-model="exp.languageLevel.arabic"
											name="languageLevelArabic"
											value="intermediary"
										/>
										<span>Intermedière</span>
									</label>
								</div>
								<div class="control">
									<label for="beginningArabic">
										<input
											type="radio"
											id="beginningArabic"
											v-model="exp.languageLevel.arabic"
											name="languageLevelArabic"
											value="beginning"
										/>
										<span>Débutant.e</span>
									</label>
								</div>
							</template>
						</div>
						<div class="col s3">
							<div class="control">
								<label for="other">
									<input
										type="checkbox"
										class
										v-model="exp.language.other"
										name="language"
										value="other"
										id="other"
									/>
									<span>Autre</span>
								</label>
								<input
									v-if="exp.language.other == true"
									v-model="exp.language.otherlanguage"
									type="text"
									placeholder="Quel autre langue ?"
									v-validate="'required'"
									class="input is-inline"
									name="otherlanguage"
								/>
							</div>
							<template v-if="exp.language.other">
								<div class="control">
									<label for="advancedOther">
										<input
											type="radio"
											id="advancedOther"
											v-model="exp.languageLevel.other"
											name="languageLevelOther"
											value="advanced"
										/>
										<span>Avancé</span>
									</label>
								</div>
								<div class="control">
									<label for="intermediaryOther">
										<input
											type="radio"
											id="intermediaryOther"
											v-model="exp.languageLevel.other"
											name="languageLevelOther"
											value="intermediary"
										/>
										<span>Intermedière</span>
									</label>
								</div>
								<div class="control">
									<label for="beginningOther">
										<input
											type="radio"
											id="beginningOther"
											v-model="exp.languageLevel.other"
											name="languageLevelOther"
											value="beginning"
										/>
										<span>Débutant.e</span>
									</label>
								</div>
							</template>
						</div>
					</div>
				</div>
				<div class="row" v-if="exp.language.english === true">
					<h2>Expliquez-nous en anglais vos motivations pour participer à notre formation. *</h2>
					<textarea
						v-model="exp.language.englishtext"
						name="english"
						id
						cols="30"
						rows="10"
						class="materialize-textarea"
					></textarea>
				</div>
			</form>
			<div class="center">
				<BaseButton :func="goBack">Précédent</BaseButton>
				<BaseButton :func="validate">Suivant</BaseButton>
			</div>
		</div>
	</div>
</template>
<style scoped>
.field,
.row {
	text-align: left;
}
h2 {
	font-size: 16px;
	font-weight: bold;
	text-transform: uppercase;
}
h1 {
	font-size: 25px;
	font-weight: bold;
	text-transform: uppercase;
}
.field {
	margin-top: 20px !important;
}
.error {
	text-align: left;
	color: red;
}
</style>